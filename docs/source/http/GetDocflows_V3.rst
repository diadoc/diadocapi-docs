GetDocflows (версия 3)
======================

Метод возвращает список документов по их идентификаторам. Для каждого документа в выдачу попадают данные, характеризующие его текущее состояние, такие как информация о документообороте и метаданные.

Для использования метода текущий пользователь должен иметь доступ ко всем документам организации.

Вся информация, относящаяся к данной цепочке (в частности, документы и подписи), по возможности помещается в протобуфер. Суммарный размер бинарных представлений (структура Content, поле Data) не может превышать 1 048 576 байт. Если добавление очередного бинарного представления вызовет превышение этого ограничения, то это бинарное представление не будет добавлено в протобуфер. Максимальное количество документов в запросе - 100.

HTTP
~~~~

.. http:post:: /V3/GetDocflows

    :query boxId: идентификатор ящика

    :reqheader Authorization: необходимые данными для :doc:`авторизации <../Authorization>`

    :statuscode 200: операция успешно завершена
    :statuscode 400: данные в запросе имеют неверный формат или отсутствуют обязательные параметры
    :statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization``, или в этом заголовке содержатся некорректные авторизационные данные
    :statuscode 403: доступ к ящику с предоставленным авторизационным токеном запрещен, либо у пользователя недостаточно прав для доступа ко всем документам организации
    :statuscode 404: в указанном ящике нет документов с указанными идентификаторами.
    :statuscode 405: используется неподходящий HTTP-метод
    :statuscode 500: при обработке запроса возникла непредвиденная ошибка

**Тело запроса:** протобуфер :doc:`../proto/GetDocflowBatchRequest`.

**Тело ответа:** протобуфер :doc:`../proto/GetDocflowBatchResponseV3`.

SDK
~~~

.. code-block:: csharp

    GetDocflowBatchResponseV3 GetDocflows(string authToken, string boxId, GetDocflowBatchRequest request);

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
    var response = api.Docflow.GetDocflows(token, boxId, request);
    foreach (var doc in response.Documents)
        Console.Out.WriteLine(doc.Docflow.SenderTitle.IsFinished);
