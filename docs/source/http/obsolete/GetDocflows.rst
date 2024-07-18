GetDocflows
===========

.. warning::
	Эта версия метода устарела. Используйте новую версию метода :doc:`../GetDocflows_V3`.

Метод ``GetDocflows`` возвращает список документов с информацией о документообороте по их идентификаторам. Для каждого документа возвращаются данные, которые характеризуют его текущее состояние: информация о документообороте и метаданные.

.. http:post:: /V2/GetDocflows

	:queryparam boxId: идентификатор :doc:`ящика <../../entities/box>` организации.

	:requestheader Authorization: данные, необходимые для :doc:`авторизации <../../Authorization>`.

	:request Body: Тело запроса должно содержать список стурктуру :doc:`../../proto/GetDocflowBatchRequest`.

	:statuscode 200: операция успешно завершена.
	:statuscode 400: данные в запросе имеют неверный формат или отсутствуют обязательные параметры.
	:statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization`` или в этом заголовке содержатся некорректные авторизационные данные.
	:statuscode 402: у организации с указанным идентификатором ``boxId`` закончилась подписка на API.
	:statuscode 403: доступ к ящику с предоставленным авторизационным токеном запрещен или у пользователя нет прав для доступа ко всем документам организации.
	:statuscode 404: в указанном ящике нет документов с указанными идентификаторами.
	:statuscode 405: используется неподходящий HTTP-метод.
	:statuscode 500: при обработке запроса возникла непредвиденная ошибка.

	:response Body: Тело ответа содержит список документов с информацией о документообороте, представленный структурой :doc:`../../proto/obsolete/GetDocflowBatchResponse`.

Метод добавляет в ответ всю информацию, относящуюся к цепочке документооборота, в том числе бинарные представления документов и подписей. Но метод имеет ограничение на суммарный размер всех бинарных представлений, хранящихся в поле ``GetDocflowBatchResponse.Documents.Docflow.DocumentAttachment.Attachment.Entity.Content.Data``, — он не должен превышать 1048576 байт. Если при добавлении очередного бинарного представления суммарный размер превысит это значение, то оно не будет добавлено в ответ метода. Вы можете получить такое бинарное представление с помощью метода :doc:`../GetEntityContent`.

Для выполнения метода текущий пользователь должен иметь доступ ко всем документам организации, иначе метод вернет ошибку ``403 (Forbidden)``.

SDK
"""

.. code-block:: csharp

    GetDocflowBatchResponse GetDocflows(string authToken, string boxId, GetDocflowBatchRequest request);

Пример использования (C#)
^^^^^^^^^^^^^^^^^^^^^^^^^

Получение двух документов и вывод на консоль признака завершенности их документооборота.

.. code-block:: csharp

    var request = new GetDocflowBatchRequest
    {
        Requests =
        {
            new GetDocflowRequest
            {
                DocumentId = new DocumentId(messageId1, documentId1),
                InjectEntityContent = true
            },
            new GetDocflowRequest
            {
                DocumentId = new DocumentId(messageId2, documentId2),
                InjectEntityContent = false,
                LastEventId = lastEventId
            }
        }
    };
    var response = api.GetDocflows(token, boxId, request);
    foreach (var doc in response.Documents)
        Console.Out.WriteLine(doc.Docflow.IsFinished);

----

.. rubric:: См. также

*Структуры и методы для работы с Docflow:*
	- :doc:`../../Docflow API`