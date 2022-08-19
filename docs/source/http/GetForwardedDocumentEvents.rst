GetForwardedDocumentEvents
==========================
 
Метод ``GetForwardedDocumentEvents`` возвращает список событий пересылки документов в ящик ``boxId``.
 
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

			- ``Filter`` — фильтр событий, представленный структурой :doc:`../proto/TimeBasedFilter`.
			- ``AfterIndexKey`` — уникальный ключ, позволяющий итерироваться по списку событий.
			- ``PopulateForwardedDocuments`` — флаг, указывающий, что в ответе нужно заполнить метаифнормацию о документах. Метаинформация возвращается в поле ``ForwardedDocument`` структуры ``ForwardedDocumentEvent``.
			- ``InjectEntityContent`` — флаг, указывающий, что в ответе нужно вернуть содержимое документа и содержимое относящихся к нему сущностей.

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

			- ``TotalCount`` — количество событий, удовлетворяющих запросу.
			- ``Events`` — список событий.
			- ``TotalCountType`` — параметр, отражающий, какое значение содержит поле ``TotalCount``, представленный структурой :doc:`<../proto/TotalCountType>`.
			- ``Timestamp`` — метка времени возникновения события, представленная структурой :doc:`<../proto/Timestamp>`.
			- ``ForwardedDocumentId`` — идентификатор пересланного документа, представленный структурой :doc:`ForwardedDocumentId <../proto/ForwardedDocument>`.
			- ``IndexKey`` — ключ, который можно передавать в качестве параметра ``AfterIndexKey`` для итерирования по отфильтрованному списку.
			- ``ForwardedDocument`` — описание пересланного документа, представленное структурой :doc:`ForwardedDocument <../proto/ForwardedDocument>`.

Список ``GetForwardedDocumentEventsResponse.Events`` может содержать не более 100 элементов. Чтобы получить остальные элементы, вызовите метод ``GetForwardedDocumentEvents`` с теми же параметрами и с указанием ``AfterIndexKey``. В зависимости от значения параметра ``AfterIndexKey`` метод работает следующим образом:

- Если в запросе отсутствует параметр ``AfterIndexKey``, то метод вернет начало списка событий, удовлетворяющих фильтру.

- Если в запросе указан параметр ``AfterIndexKey``, то возвращенный список начнется с события, следующего за событием с ключом ``AfterIndexKey``; событие с ключом ``AfterIndexKey`` в этот список не попадает.

Пример использования (C#)
^^^^^^^^^^^^^^^^^^^^^^^^^

Получение списка пересланных документов.

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


----

.. rubric:: Смотри также

*Другие методы для работы с событиями:*
	- :doc:`GetNewEvents` — возвращает ленту событий в ящике.
	- :doc:`GetEvent` — возвращает информацию о конкретном событии.
	- :doc:`GetLastEvent` — возвращает последнее событие в ящике.