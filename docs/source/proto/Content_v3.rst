Content_v3
==========

Структура описывает данные (содержимое документа, файла) либо как массив байтов, либо как ссылку на загруженный файл в Диадоке.

.. code-block:: protobuf

	message Content_v3 {
		optional bytes Content = 1;
		optional string NameOnShelf = 2;
		optional DocumentId EntityId = 3;
		optional string PatchedContentId = 4;
	}

- ``Content`` — данные как массив байтов.
- ``NameOnShelf`` — имя файла на полке. Подробно про загрузку на полку в описании метода :doc:`../http/ShelfUpload`.
- ``EntityId`` — идентификатор сущности, представленный структурой :doc:`DocumentId`.
- ``PatchedContentId`` — идентификатор документа, подготовленного к отправке методом :doc:`../http/PrepareDocumentsToSign`.

В структуре должно быть заполнено только одно из перечисленных выше полей.