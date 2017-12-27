DetectDocumentTypes
===================

Метод возвращает возможные типы переданного документа.

.. http:post:: /DetectDocumentTypes

    :query boxId: идентификатор ящика
    :query nameOnShelf: имя файла на «полке документов»

    :body: содержимое документа

    :reqheader Authorization: необходимые данные для :doc:`авторизации <../Authorization>`

    :statuscode 200: операция успешно завершена
    :statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization``, или в этом заголовке содержатся некорректные авторизационные данные
    :statuscode 403: доступ к ящику с предоставленным авторизационным токеном запрещен
    :statuscode 404: не найден ящик по переданному `boxId` 
    :statuscode 500: при обработке запроса возникла непредвиденная ошибка


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
