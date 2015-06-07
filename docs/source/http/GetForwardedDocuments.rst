GetForwardedDocuments
=====================

Имя ресурса: **/V2/GetForwardedDocuments**

HTTP метод: **POST**

Параметры строки запроса:

-  *boxId* - идентификатор ящика;

В запросе должен присутствовать HTTP-заголовок ``Authorization`` с необходимыми данными для :doc:`авторизации <../Authorization>`.

Тело запроса должно содержать сериализованный протобуфер *GetForwardedDocumentsRequest*:

.. code-block:: protobuf

    message GetForwardedDocumentsRequest
    {
        repeated ForwardedDocumentId ForwardedDocumentIds = 1;
        optional bool InjectEntityContent = 2 [default = false];
    }
            

Тело ответа будет содержать сериализованный протобуфер *GetForwardedDocumentsResponse*:

.. code-block:: protobuf

    message GetForwardedDocumentsResponse
    {
        repeated ForwardedDocument ForwardedDocuments = 1;
    }
            

Метод позволяет получить пересланные в ящик boxId документы, зная их идентификаторы. Идентификаторы документов в запросе описываются структурой :doc:`ForwardedDocumentId <../proto/ForwardedDocument>`.

Документы в ответе описываются структурой :doc:`../proto/ForwardedDocument`.

Флаг *GetForwardedDocumentsRequest.InjectEntityContent* управляет тем, будет ли сервер вместе с метаинформацией о документе возвращать его контент и контент относящихся к нему сущностей.

Возможные HTTP-коды возврата:

-  200 (OK) - операция успешно завершена;

-  400 (Bad Request) - данные в запросе имеют неверный формат или отсутствуют обязательные параметры;

-  401 (Unauthorized) - в запросе отсутствует HTTP-заголовок ``Authorization``, или в этом заголовке содержатся некорректные авторизационные данные;

-  403 (Forbidden) - доступ к ящику с предоставленным авторизационным токеном запрещен;

-  404 (Not found) - не найдено сообщение/документ с заданным идентификатором;

-  405 (Method not allowed) - используется неподходящий HTTP-метод;

-  500 (Internal server error) - при обработке запроса возникла непредвиденная ошибка.