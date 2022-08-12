GetForwardedDocumentEvents
==========================
 
Метод ``GetForwardedDocumentEvents`` предназначен для получения списка событий пересылки документов в ящик ``boxId``.
 
.. http:post:: /V2/GetForwardedDocumentEvents

	:queryparam boxId: идентификатор ящика организации.

	:requestheader Authorization: данные, необходимые для :doc:`авторизации <../Authorization>`.

	:Request Body: Тело запроса должно содержать структуру ``GetForwardedDocumentEventsRequest``:

            .. code-block:: protobuf

                message GetForwardedDocumentEventsRequest
                {
                    required TimeBasedFilter Filter = 1;
                    optional bytes AfterIndexKey = 2;
                    optional bool PopulateForwardedDocuments = 3 [default = false];
                    optional bool InjectEntityContent = 4 [default = false];
                }
            ..

			- ``TimeBasedFilter`` — фильтр событий описывается структурой :doc:`../proto/TimeBasedFilter`.
			- ``AfterIndexKey`` — позволяет итерироваться по всему списку документов, удовлетворяющих фильтру.
			- ``PopulateForwardedDocuments`` — флаг отвечает за то, будет ли сервер в списке событий заполнять метаинформацию о документах.
			- ``InjectEntityContent`` — флаг отвечает за то, будет ли сервер вместе с метаинформацией о документе возвращать его контент и контент относящихся к нему сущностей.

	:statuscode 200: операция успешно завершена.
	:statuscode 400: данные в запросе имеют неверный формат или отсутствуют обязательные параметры.
	:statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization`` или в этом заголовке содержатся некорректные авторизационные данные.
	:statuscode 402: у организации с указанным идентификатором ``boxId`` закончилась подписка на API.
	:statuscode 403: доступ к ящику с предоставленным авторизационным токеном запрещен.
	:statuscode 404: не найдено сообщение с заданным идентификатором.
	:statuscode 405: используется неподходящий HTTP-метод.
	:statuscode 500: при обработке запроса возникла непредвиденная ошибка.

	:response Body: Тело ответа содержит результат выполнения операции, представленный структурой  ``GetForwardedDocumentEventsResponse``:

            .. code-block:: protobuf

                message GetForwardedDocumentEventsResponse
                {
                    required int32 TotalCount = 1;
                    repeated ForwardedDocumentEvent Events = 2;
                    required TotalCountType TotalCountType = 3;
                }
 
                message ForwardedDocumentEvent
                {
                    required Timestamp Timestamp = 1;
                    required ForwardedDocumentId ForwardedDocumentId = 2;
                    required bytes IndexKey = 3;
                    optional ForwardedDocument ForwardedDocument = 4;
                }
            ..

			- ``IndexKey`` — ключ, который можно передавать в качестве параметра ``afterIndexKey`` для итерирования по всему отфильтрованному списку.

Пример использования
^^^^^^^^^^^^^^^^^^^^
 
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
           