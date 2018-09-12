DocumentList
============

.. code-block:: protobuf

    message DocumentList {
        required int32 TotalCount = 1;
        repeated Document Documents = 2;
        required bool HasMoreResults = 3;
    }
        

Структура данных DocumentList представляет собой список документов, возвращаемый методом :doc:`../http/GetDocuments`. 
Поле DocumentList.TotalCount содержит общее количество документов, удовлетворяющих фильтру. Если количество документов превышает 1000, значение TotalCount всегда будет возвращаться равным 1000 и признак HasMoreResults=true. Если документов менее 1000, в TotalCount будет возвращаться точное количество документов, признак HasMoreResults = false. 
Каждый элемент списка DocumentList.Documents представлен структурой :doc:`Document`.

