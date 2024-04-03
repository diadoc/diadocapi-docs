DetectDocumentTitles
====================

Метод ``DetectDocumentTitles`` определяет возможные типы указанного документа.

.. http:post:: /DetectDocumentTitles

	:queryparam boxId: идентификатор :doc:`ящика <../entities/box>` организации.

	:request Body: Тело запроса должно содержать бинарные данные документа.


.. http:get:: /DetectDocumentTitles

	:queryparam boxId: идентификатор :doc:`ящика <../entities/box>` организации.
	:queryparam nameOnShelf: имя файла на :doc:`полке документов<../entities/shelf>`.

	:requestheader Authorization: данные, необходимые для :doc:`авторизации <../Authorization>`.

	:statuscode 200: операция успешно завершена.
	:statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization`` или в этом заголовке содержатся некорректные авторизационные данные.
	:statuscode 402: у организации с указанным идентификатором ``boxId`` закончилась подписка на API.
	:statuscode 403: доступ к ящику с предоставленным авторизационным токеном запрещен.
	:statuscode 404: не найден ящик с указанным идентификатором.
	:statuscode 500: при обработке запроса возникла непредвиденная ошибка.

	:response Body: Тело ответа содержит массив с описаниями типов документов, представленное структурой ``DetectTitleResponse``:

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

		..
		
Метод можно использовать двумя способами:

    - POST-запрос с заполненным ``Request Body``,
    - GET-запрос с параметром ``nameOnShelf``, если содержимое документа было загружено на полку методом :doc:`../http/ShelfUpload`.


Метод анализирует содержимое документа и определяет, с какими значениями ``TypeNamedId`` можно отправить документ с таким содержимым.
Если таких типов несколько, то метод вернет массив с описанием всех этих типов. Так бывает в случае, когда у нескольких типов документов схожее содержимое. Например, накладную в 820 формате можно отправить с типами ``UniversalTransferDocument`` и ``XmlTorg12``. В этом случае для накладной в 820 формате вернется массив с двумя типами документов.
Если содержимому документа соответствует только один тип, то метод вернет массив с единственным элементом.

.. note::
	Метод будет определять только те типы документов, которые доступны в текущей организации.
