Content_v3
==========

Структура ``Content_v3`` представляет собой содержимое документа.

Содержимое может храниться в структуре в виде бинарных данных или может быть представлено ссылкой на документ, хранящийся на :doc:`полке документов<../entities/shelf>`.

.. code-block:: protobuf

	message Content_v3 {
		optional bytes Content = 1;
		optional string NameOnShelf = 2;
		optional DocumentId EntityId = 3;
		optional string PatchedContentId = 4;
	}

- ``Content`` — содержимое в виде бинарных данных.
- ``NameOnShelf`` — имя файла на :doc:`полке документов<../entities/shelf>`.
- ``EntityId`` — идентификатор сущности, представленный структурой :doc:`DocumentId`.
- ``PatchedContentId`` — идентификатор документа, подготовленного к отправке методом :doc:`../http/PrepareDocumentsToSign`.

В структуре должно быть заполнено только одно из перечисленных выше полей.