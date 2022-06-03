Content_v2
===========

Структура ``Content_v2`` представляет собой содержимое документов и файлов как массив байтов или как ссылку в Диадоке.

.. code-block:: protobuf

	message Content_v2 {
		optional bytes Content = 1;
		optional string NameOnShelf = 2;
		optional string PatchedContentId = 3;
	}

- ``Content`` — данные как массив байтов.
- ``NameOnShelf`` — имя файла на полке. Подробно про загрузку на полку в описании метода :doc:`../http/ShelfUpload`.
- ``PatchedContentId`` — идентификатор документа, подготовленного к отправке методом :doc:`../http/PrepareDocumentsToSign`.