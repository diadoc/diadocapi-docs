GetDocflowEvents (версия 3)
===========================

Метод возвращает список событий, произошедших с документами в указанном ящике. Под событием понимается возникновение нового документа, либо изменение уже существующего.

Каждое событие в выдаче содержит состояние документа на момент этого события, и, опционально, состояние на момент предыдущего события. Это позволяет сравнивать две версии документа и вычислять произошедшие изменения.

Максимальное количество возвращаемых событий в рамках одного запроса равно 100. Если событий в ящике больше, их можно выгрузить постранично.
Для этого в метод передается специальный ключ, служащий индикатором события, с которого нужно начинать очередную выгрузку (см. :doc:`../proto/GetDocflowEventsRequest`).

Вся информация, относящаяся к данной цепочке событий (в частности, документы и подписи), по возможности помещаются в протобуфер (информацию о том, в каких случаях возвращаемая цепочка может не содержать бинарного представления документов см. в описании структуры :doc:`../proto/Content`).

В тех ситуациях, когда для каких-то документов цепочки документооборота бинарное представление не было выдано (по причине большого размера), его всегда можно получить при помощи метода :doc:`GetEntityContent`.

HTTP
~~~~

.. http:post:: /V3/GetDocflowEvents

    :query boxId: идентификатор ящика;

    :reqheader Authorization: необходимые данными для :doc:`авторизации <../Authorization>`

    :statuscode 200: операция успешно завершена
    :statuscode 400: данные в запросе имеют неверный формат или отсутствуют обязательные параметры
    :statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization``, или в этом заголовке содержатся некорректные авторизационные данные
    :statuscode 403: доступ к ящику с предоставленным авторизационным токеном запрещен, либо у пользователя недостаточно прав для доступа ко всем документам организации
    :statuscode 405: используется неподходящий HTTP-метод
    :statuscode 500: при обработке запроса возникла непредвиденная ошибка

**Тело запроса:** протобуфер :doc:`../proto/GetDocflowEventsRequest`.

**Тело ответа:** протобуфер :doc:`../proto/GetDocflowEventsResponseV3`.

SDK
~~~

.. code-block:: csharp

    GetDocflowEventsResponseV3 GetDocflowEvents(string authToken, string boxId, GetDocflowEventsRequest request);

Пример использования (C#)
^^^^^^^^^^^^^^^^^^^^^^^^^

Получение всех событий в ящике за период с 13.11.2013 до 20.11.2013:

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
