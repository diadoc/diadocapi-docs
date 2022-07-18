DetectDocumentTypes
===================

Метод ``DetectDocumentTypes`` возвращает возможные типы переданного документа.

.. warning::
	Метод считается устаревшим и не рекомендуются к использованию, т.к. он умеет детектировать только первые титулы документов. Вместо него используйте более универсальный метод :doc:`../http/DetectDocumentTitles`

.. http:post:: /DetectDocumentTypes

	:queryparam boxId: идентификатор ящика организации.
	:queryparam nameOnShelf: имя файла на «полке документов».

	:requestheader Authorization: данные, необходимые для :doc:`авторизации <../Authorization>`.

	:request Body: Тело запроса должно хранить содержимое документа.

	:statuscode 200: операция успешно завершена.
	:statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization`` или в этом заголовке содержатся некорректные авторизационные данные.
	:statuscode 402: у организации с указанным идентификатором ``boxId`` закончилась подписка на API.
	:statuscode 403: доступ к ящику с предоставленным авторизационным токеном запрещен.
	:statuscode 404: не найден ящик с указанным идентификатором.
	:statuscode 500: при обработке запроса возникла непредвиденная ошибка.

Метод можно использовать в двух случаях:

    - `POST` запрос с заполненным `body`
    - `GET` запрос с `nameOnShelf` параметром

Тело ответа будет содержать структуру *DetectDocumentTypesResponse* с описанием типов документов:

.. code-block:: protobuf

    message DetectDocumentTypesResponse {
        repeated DetectedDocumentType DocumentTypes = 1;
    }

    message DetectedDocumentType {
        required string TypeNamedId = 1;
        required string Function = 2;
        required string Version = 3;
    }
