GetDocflowEvents
================

Метод возвращает список событий, произошедших с документами в указанном ящике. Под событием понимается возникновение нового документа, либо изменение уже существующего.

Каждое событие в выдаче содержит состояние документа на момент этого события, и, опционально, состояние на момент предыдущего события. Это позволяет сравнивать две версии документа и вычислять произошедшие изменения.

Максимальное количество возвращаемых событий в рамках одного запроса равно 100. Если событий в ящике больше, их можно выгрузить постранично.
Для этого в метод передается специальный ключ, служащий индикатором события, с которого нужно начинать очередную выгрузку (см.[[GetDocflowEventsRequest]]).

Для использования метода текущий пользователь должен иметь доступ ко всем документам организации.

HTTP
~~~~

**POST /V2/GetDocflowEvents**

**Параметры запроса:**

-  *boxId* - идентификатор ящика

**Тело запроса:** протобуфер :doc:`../proto/GetDocflowEventsRequest`.

**Тело ответа:** протобуфер :doc:`../proto/GetDocflowEventsResponse`.

**Возможные HTTP-коды возврата:**

-  *200 (OK)* - операция успешно завершена.
-  *400 (Bad Request)* - данные в запросе имеют неверный формат или отсутствуют обязательные параметры.
-  *401 (Unauthorized)* - в запросе отсутствует HTTP-заголовок ``Authorization``, или в этом заголовке содержатся некорректные авторизационные данные.
-  *403 (Forbidden)* - доступ к ящику с предоставленным авторизационным токеном запрещен, либо у пользователя недостаточно прав для доступа ко всем документам организации.
-  *405 (Method not allowed)* - используется неподходящий HTTP-метод.
-  *500 (Internal server error)* - при обработке запроса возникла непредвиденная ошибка.

SDK
~~~

.. code-block:: csharp

    GetDocflowEventsResponse GetDocflowEvents(string authToken, string boxId, GetDocflowEventsRequest request);

Пример использования (C#)
^^^^^^^^^^^^^^^^^^^^^^^^^

Получение всех событий в ящике за период с 13.11.2013 до 20.11.2013:

.. code-block:: csharp

    byte[] indexKey = null;
    while (true)
    {
        var request = new GetDocflowEventsRequest
        {
            FromTimestamp = new Timestamp(new DateTime(2013, 11, 13).Ticks), // может отсутствовать
            ToTimestamp = new Timestamp(new DateTime(2013, 11, 20).Ticks), // может отсутствовать
            AfterIndexKey = indexKey
        };
        var response = api.GetDocflowEvents(token, boxId, request);
        if (!response.Events.Any())
            break;
        Console.Out.WriteLine("Events count: {0} (of total {1})", response.Events.Count, response.TotalCount);
        indexKey = response.Events.Last().IndexKey;
    }
