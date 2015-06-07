GetForwardedDocumentEvents
==========================

Имя ресурса: **/V2/GetForwardedDocumentEvents**

HTTP метод: **POST**

Параметры строки запроса:

-  *boxId* - идентификатор ящика;

В запросе должен присутствовать HTTP-заголовок ``Authorization`` с необходимыми данными для :doc:`авторизации <../Authorization>`.

Тело запроса должно содержать сериализованный протобуфер *GetForwardedDocumentEventsRequest*:

.. code-block:: protobuf

    message GetForwardedDocumentEventsRequest
    {
        required TimeBasedFilter Filter = 1;
        optional bytes AfterIndexKey = 2;
        optional bool PopulateForwardedDocuments = 3 [default = false];
        optional bool InjectEntityContent = 4 [default = false];
    }
            

Тело ответа будет содержать сериализованный протобуфер *GetForwardedDocumentEventsResponse*:

.. code-block:: protobuf

    message GetForwardedDocumentEventsResponse
    {
        required int32 TotalCount = 1;
        repeated ForwardedDocumentEvent Events = 2;
    }

    message ForwardedDocumentEvent
    {
        required Timestamp Timestamp = 1;
        required ForwardedDocumentId ForwardedDocumentId = 2;
        required bytes IndexKey = 3;
        optional ForwardedDocument ForwardedDocument = 4;
    }
            

Метод позволяет получить список событий пересылки документов в ящик *boxId*.

Фильтр событий в запросе описывается структурой :doc:`../proto/TimeBasedFilter`. События в ответе описываются структурой *ForwardedDocumentEvent*.

Поле *ForwardedDocumentEvent.IndexKey* можно использовать для итерирования списка, заполняя его значением поле *GetForwardedDocumentEventsRequest.AfterIndexKey*.

Флаг *GetForwardedDocumentEventsRequest.PopulateForwardedDocuments* управляет тем, будет ли сервер в выдаваемом списке событий заполнять метаинформацию о соответствующих документах (поле *ForwardedDocumentEvent.ForwardedDocument*).

Флаг *GetForwardedDocumentEventsRequest.InjectEntityContent* управляет тем, будет ли сервер вместе с метаинформацией о документе возвращать его контент и контент относящихся к нему сущностей.

Возможные HTTP-коды возврата:

-  200 (OK) - операция успешно завершена;

-  400 (Bad Request) - данные в запросе имеют неверный формат или отсутствуют обязательные параметры;

-  401 (Unauthorized) - в запросе отсутствует HTTP-заголовок ``Authorization``, или в этом заголовке содержатся некорректные авторизационные данные;

-  403 (Forbidden) - доступ к ящику с предоставленным авторизационным токеном запрещен;

-  404 (Not found) - не найдено сообщение/документ с заданным идентификатором;

-  405 (Method not allowed) - используется неподходящий HTTP-метод;

-  500 (Internal server error) - при обработке запроса возникла непредвиденная ошибка.

Пример вычитывания списка пересланных документов

.. code-block:: csharp

	var diadoc = new DiadocApi(...);
	var authToken = ...;
	var myBoxId = ...;

    var request = new GetForwardedDocumentEventsRequest { PopulateForwardedDocuments = true };
    while (true)
    {
        var response = diadoc.GetForwardedDocumentEvents(authToken, myBoxId, request);
        foreach (var forwardEvent in response.Events)
        {
            var docInfo = forwardEvent.ForwardedDocument.DocumentWithDocflow.DocumentInfo;
            Console.WriteLine("Document type: {0}, number: {1}, date: {2}", docInfo.DocumentType,
                docInfo.DocumentDateAndNumber.DocumentNumber, docInfo.DocumentDateAndNumber.DocumentDate);
        }
        if (response.Events.Count == 0)
            break;
        request.AfterIndexKey = response.Events.Last().IndexKey;
    }
            
