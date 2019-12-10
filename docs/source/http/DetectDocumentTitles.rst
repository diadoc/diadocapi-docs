DetectDocumentTitles
====================

Метод возвращает возможные типы переданного документа.

.. http:post:: /DetectDocumentTitles

    :query boxId: идентификатор ящика
    :body: бинарное содержимое документа

.. http:get:: /DetectDocumentTitles

    :query boxId: идентификатор ящика
    :query nameOnShelf: имя файла на «полке документов»

    :reqheader Authorization: необходимые данные для :doc:`авторизации <../Authorization>`

    :statuscode 200: операция успешно завершена
    :statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization``, или в этом заголовке содержатся некорректные авторизационные данные
    :statuscode 403: доступ к ящику с предоставленным авторизационным токеном запрещен
    :statuscode 404: не найден ящик по переданному `boxId` 
    :statuscode 500: при обработке запроса возникла непредвиденная ошибка    


Метод можно использовать в двух случаях:

    - `POST` запрос с заполненным `body`
    - `GET` запрос с `nameOnShelf` параметром, если контент был загружен на полку через :doc:`../http/ShelfUpload`

Тело ответа будет содержать структуру *DetectTitleResponse* с описанием типов документов:

.. code-block:: protobuf

    message DetectTitleResponse {
        repeated DetectedDocumentTitle DocumentTitles = 1;
    }
    
    message DetectedDocumentTitle {
        required string TypeNamedId = 1;
        required string Function = 2;
        required string Version = 3;
        required int32 TitleIndex = 4;
        repeated Events.MetadataItem Metadata = 5;
    }

.. note:: Метод будет пытаться детектировать только по тем типам документов, которые доступны в конкретной организации.
