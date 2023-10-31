Content_v2
===========

Структура ``Content_v2`` представляет собой содержимое документа.

Содержимое может храниться в структуре в виде бинарных данных или может быть представлено ссылкой на документ, хранящийся на :doc:`полке документов<../entities/shelf>`.

.. code-block:: protobuf

	message Content_v2 {
		optional bytes Content = 1;
		optional string NameOnShelf = 2;
		optional string PatchedContentId = 3;
	}

- ``Content`` — содержимое в виде бинарных данных.
- ``NameOnShelf`` — имя файла на :doc:`полке документов<../entities/shelf>`.
- ``PatchedContentId`` — идентификатор документа, подготовленного к отправке методом :doc:`../http/PrepareDocumentsToSign`.