GetDocflows
===========

Метод возвращает список документов по их идентификаторам. Для каждого документа в выдачу попадают данные, характеризующие его текущее состояние, такие как информация о документообороте и метаданные.

Для использования метода текущий пользователь должен иметь доступ ко всем документам организации.

Вся информация, относящаяся к данной цепочке (в частности, документы и подписи), по возможности помещается в протобуфер. Суммарный размер бинарных представлений (структура Content, поле Data) не может превышать 1 048 576 байт. Если добавление очередного бинарного представления вызовет превышение этого ограничения, то это бинарное представление не будет добавлено в протобуфер.

HTTP
~~~~

**POST /V2/GetDocflows**

**Параметры запроса:**

-  *boxId* - идентификатор ящика

**Тело запроса:** протобуфер :doc:`../proto/GetDocflowBatchRequest`.

**Тело ответа:** протобуфер :doc:`../proto/GetDocflowBatchResponse`.

**Возможные HTTP-коды возврата:**

-  *200 (OK)* - операция успешно завершена.
-  *400 (Bad Request)* - данные в запросе имеют неверный формат или отсутствуют обязательные параметры.
-  *401 (Unauthorized)* - в запросе отсутствует HTTP-заголовок ``Authorization``, или в этом заголовке содержатся некорректные авторизационные данные.
-  *403 (Forbidden)* - доступ к ящику с предоставленным авторизационным токеном запрещен, либо у пользователя недостаточно прав для доступа
   ко всем документам организации.
-  *404 (Not Found)* - в указанном ящике нет документов с указанными идентификаторами.
-  *405 (Method not allowed)* - используется неподходящий HTTP-метод.
-  *500 (Internal server error)* - при обработке запроса возникла непредвиденная ошибка.

SDK
~~~

.. code-block:: csharp

    GetDocflowBatchResponse GetDocflows(string authToken, string boxId, GetDocflowBatchRequest request);

Пример использования (C#)
^^^^^^^^^^^^^^^^^^^^^^^^^

Выгрузка двух документов и вывод на консоль признака завершенности их
документооборота:

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
