ForwardDocument
===============

Имя ресурса: **/V2/ForwardDocument**

HTTP метод: **POST**

Параметры строки запроса:

-  *boxId* - идентификатор ящика;

В запросе должен присутствовать HTTP-заголовок ``Authorization`` с необходимыми данными для :doc:`авторизации <../Authorization>`.

Тело запроса должно содержать сериализованный протобуфер *ForwardDocumentRequest*:

.. code-block:: protobuf

    message ForwardDocumentRequest
    {
        required string ToBoxId = 1;
        required DocumentId DocumentId = 2;
    }

В теле ответа содержится сериализованный протобуфер ForwardDocumentResponse:

.. code-block:: protobuf

    message ForwardDocumentResponse
    {
    	optional Timestamp ForwardTimestamp = 1;
    	optional ForwardedDocumentId ForwardedDocumentId = 2;
    }

Метод позволяет переслать документ *ForwardDocumentRequest.DocumentId* из ящика boxId третьей стороне (в ящик *ForwardDocumentRequest.ToBoxId*).

При этом адресат пересылки получает снэпшот состояния документа на текущий момент времени. Допускается пересылка одного документа нескольким получателям, а также - пересылка одного документа несколько раз одному получателю.

Возможные HTTP-коды возврата:

-  200 (OK) - операция успешно завершена;

-  400 (Bad Request) - данные в запросе имеют неверный формат или отсутствуют обязательные параметры;

-  401 (Unauthorized) - в запросе отсутствует HTTP-заголовок ``Authorization``, или в этом заголовке содержатся некорректные авторизационные данные;

-  403 (Forbidden) - доступ к ящику с предоставленным авторизационным токеном запрещен;

-  404 (Not found) - не найдено сообщение/документ с заданным идентификатором;

-  405 (Method not allowed) - используется неподходящий HTTP-метод;

-  409 (Conflict) - текущее состояние системы не позволяет корректно обработать запрос или запрещен прием документов от контрагентов согласно свойству ``Sociability`` из :doc:`../proto/Organization`.;

-  500 (Internal server error) - при обработке запроса возникла непредвиденная ошибка.
