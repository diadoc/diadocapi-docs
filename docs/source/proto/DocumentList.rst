DocumentList
============

.. code-block:: protobuf

    message DocumentList {
        required int32 TotalCount = 1;
        repeated Document Documents = 2;
        optional bool HasMoreResults = 3;
    }
        

Структура данных DocumentList представляет собой список документов, возвращаемый методом :doc:`../http/GetDocuments` или методом :doc:`../http/GetDocumentsByMessageId`.
Каждый элемент списка DocumentList.Documents представлен структурой :doc:`Document`.

Для метода :doc:`../http/GetDocumentsByMessageId` всегда возвращаются все доступные для сотрудника документы из сообщения. Признак HasMoreResults будет всегда принимать значение false.

Для метода :doc:`../http/GetDocuments` поле DocumentList.TotalCount содержит общее количество документов, удовлетворяющих фильтру. Если количество документов превышает 1000, значение TotalCount всегда будет возвращаться равным 1000 и признак HasMoreResults=true. Если документов менее 1000, в TotalCount будет возвращаться точное количество документов, признак HasMoreResults = false. 


