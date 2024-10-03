DocumentList
============

Структура ``DocumentList`` представляет собой список документов.

.. code-block:: protobuf

    message DocumentList {
        required int32 TotalCount = 1;
        repeated Document Documents = 2;
        optional bool HasMoreResults = 3;
    }

- ``TotalCount`` — общее количество документов, удовлетворяющих запросу. В ответе метода :doc:`../http/GetDocuments` принимает значение в зависимости от количества найденных документов:

	- если документов больше 1000, то значение ``TotalCount`` будет равным 1000, а признак ``HasMoreResults`` будет иметь значение ``true``;
	- если документов меньше 1000, то в поле ``TotalCount`` вернется точное количество документов, а признак ``HasMoreResults`` будет иметь значение ``false``.

- ``Documents`` — список документов, представленный структурой :doc:`Document`.
- ``HasMoreResults`` — признак того, что найденных документов больше 1000 и в списке ``Documents`` содержатся не все найденные документы. В ответе метода :doc:`../http/GetDocumentsByMessageId` всегда имеет значение ``false``.


----

.. rubric:: См. также

*Структура используется:*
	- в теле ответа метода :doc:`../http/GetDocuments`
	- в теле ответа метода :doc:`../http/GetDocumentsByMessageId`