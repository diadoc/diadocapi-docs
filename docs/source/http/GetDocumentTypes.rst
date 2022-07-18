GetDocumentTypes
================

Метод ``GetDocumentTypes`` возвращает описание типов документов, доступных в ящике.

.. http:get:: /V2/GetDocumentTypes

	:queryparam boxId: идентификатор ящика организации.

	:requestheader Authorization: данные, необходимые для :doc:`авторизации <../Authorization>`.

	:statuscode 200: операция успешно завершена.
	:statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization`` или в этом заголовке содержатся некорректные авторизационные данные.
	:statuscode 402: у организации с указанным идентификатором ``boxId`` закончилась подписка на API.
	:statuscode 403: доступ к ящику с предоставленным авторизационным токеном запрещен.
	:statuscode 405: используется неподходящий HTTP-метод.
	:statuscode 500: при обработке запроса возникла непредвиденная ошибка.

Тело ответа будет содержать структуру *GetDocumentTypesResponseV2* с описанием типов документов:

.. code-block:: protobuf

    message GetDocumentTypesResponseV2 {
    	repeated DocumentTypeDescriptionV2 DocumentTypes = 1;
    }

- :doc:`DocumentTypes <../proto/DocumentTypeDescriptionV2>` - список типов документов.
