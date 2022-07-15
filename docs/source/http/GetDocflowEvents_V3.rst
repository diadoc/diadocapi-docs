GetDocflowEvents (версия 3)
===========================

Метод ``GetDocflowEvents`` возвращает список событий, произошедших с документами в указанном ящике. Под событием понимается появление нового документа или изменение уже существующего.

.. http:post:: /V3/GetDocflowEvents

	:queryparam boxId: идентификатор ящика организации.

	:requestheader Authorization: данные, необходимые для :doc:`авторизации <../Authorization>`.

	:request Body: Тело запроса должно содержать структуру :doc:`../proto/GetDocflowEventsRequest`.

	:statuscode 200: операция успешно завершена.
	:statuscode 400: данные в запросе имеют неверный формат или отсутствуют обязательные параметры.
	:statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization`` или в этом заголовке содержатся некорректные авторизационные данные.
	:statuscode 402: у организации с указанным идентификатором ``boxId`` закончилась подписка на API.
	:statuscode 403: доступ к ящику с предоставленным авторизационным токеном запрещен или у пользователя нет прав для доступа ко всем документам организации.
	:statuscode 405: используется неподходящий HTTP-метод.
	:statuscode 500: при обработке запроса возникла непредвиденная ошибка.

Метод возвращает список событий, представленный структурой :doc:`../proto/GetDocflowEventsResponseV3`.

Список событий в ответе может содержать не более 100 элементов. Если событий в ящике больше, их можно получить постранично. Для этого вызовите метод ``GetDocflowEvents`` с указанием параметра :doc:`GetDocflowEventsRequest.AfterIndexKey <../proto/GetDocflowEventsRequest>` в структуре запроса. Этот параметр служит индикатором события, с которого нужно начать очередную выгрузку.

Метод добавляет в ответ всю информацию, относящуюся к цепочке документооборота, в том числе бинарные представления документов и подписей, если они есть — возвращаемая цепочка может не содержать бинарного представления документов, подробнее об этом в описании структуры :doc:`../proto/Content`. Но метод имеет ограничение на суммарный размер всех бинарных представлений, хранящихся в поле ``GetDocflowEventsResponse.Events.Document.Docflow.DocumentAttachment.Attachment.Entity.Content.Data``, — он не должен превышать 1 048 576 байт.
Если при добавлении очередного бинарного представления суммарный размер превысит это значение, то оно не будет добавлено в ответ метода. Вы можете получить такое бинарное представление с помощью метода :doc:`GetEntityContent`.

Каждое событие в ответе может содержать состояние документа на момент этого события и состояние на момент предыдущего события, если вы укажете свойства ``GetDocflowEventsRequest.PopulateDocuments`` и ``GetDocflowEventsRequest.PopulatePreviousDocumentStates`` соответственно. Таким образом можно сравнить две версии документа и узнать произошедшие изменения.

Для выполнения метода текущий пользователь должен иметь доступ ко всем документам организации, иначе метод вернет ошибку ``403 (Forbidden)``.

SDK
"""

.. code-block:: csharp

    GetDocflowEventsResponseV3 GetDocflowEvents(string authToken, string boxId, GetDocflowEventsRequest request);

Пример использования (C#)
^^^^^^^^^^^^^^^^^^^^^^^^^

Получение всех событий в ящике за период с 13.11.2013 до 20.11.2013.

.. code-block:: csharp

    var request = new GetDocflowEventsRequest
    {
        Filter = new TimeBasedFilter 
        {
            FromTimestamp = new Timestamp(new DateTime(2013, 11, 13).Ticks), // может отсутствовать
            ToTimestamp = new Timestamp(new DateTime(2013, 11, 20).Ticks), // может отсутствовать
        },
        AfterIndexKey = null
    };
    while (true)
    {
        var response = api.Docflow.GetDocflowEvents(token, boxId, request);
        if (!response.Events.Any())
            break;
        Console.Out.WriteLine("Events count: {0} (of total {1})", response.Events.Count, response.TotalCount);
        request.AfterIndexKey = response.Events.Last().IndexKey;
    }