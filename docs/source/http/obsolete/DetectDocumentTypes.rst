DetectDocumentTypes
===================

.. warning::
	Метод устарел. Для определения типов используйте метод :doc:`../../http/DetectDocumentTitles`.

Метод ``DetectDocumentTypes`` определяет возможные типы указанного документа.

.. http:post:: /DetectDocumentTypes

	:queryparam boxId: идентификатор ящика организации.
	:queryparam nameOnShelf: имя файла на :doc:`полке документов<../../entities/shelf>`.

	:requestheader Authorization: данные, необходимые для :doc:`авторизации <../../Authorization>`.

	:request Body: Тело запроса должно хранить бинарное содержимое документа.

	:statuscode 200: операция успешно завершена.
	:statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization`` или в этом заголовке содержатся некорректные авторизационные данные.
	:statuscode 402: у организации с указанным идентификатором ``boxId`` закончилась подписка на API.
	:statuscode 403: доступ к ящику с предоставленным авторизационным токеном запрещен.
	:statuscode 404: не найден ящик с указанным идентификатором.
	:statuscode 500: при обработке запроса возникла непредвиденная ошибка.

	:response Body: Тело ответа содержит описание типов документов, представленное структурой ``DetectDocumentTypesResponse``:

		.. code-block:: protobuf

			message DetectDocumentTypesResponse {
				repeated DetectedDocumentType DocumentTypes = 1;
			}

			message DetectedDocumentType {
				required string TypeNamedId = 1;
				required string Function = 2;
				required string Version = 3;
			}
			
		..

Метод можно использовать в двух вариантах:

    - ``POST`` запрос с заполненным ``Request Body``,
    - ``GET`` запрос с параметром ``nameOnShelf``, если содержимое документа было загружено на полку методом :doc:`../../http/ShelfUpload`.