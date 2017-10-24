GetDocumentTypes
================

Метод возвращает описание типов документов, доступных в ящике.

.. http:get:: /GetDocumentTypes

    :query boxId: идентификатор ящика

    :reqheader Authorization: необходимые данные для :doc:`авторизации <../Authorization>`

    :statuscode 200: операция успешно завершена
    :statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization``, или в этом заголовке содержатся некорректные авторизационные данные
    :statuscode 403: доступ к ящику с предоставленным авторизационным токеном запрещен
    :statuscode 405: используется неподходящий HTTP-метод
    :statuscode 500: при обработке запроса возникла непредвиденная ошибка

Тело ответа будет содержать структуру *GetDocumentTypesResponse* с описанием типов документов:

.. code-block:: protobuf

    message GetDocumentTypesResponse {
    	repeated DocumentTypeDescription DocumentTypes = 1;
    }

- :doc:`DocumentTypes <../proto/DocumentTypeDescription>` - список типов документов.
