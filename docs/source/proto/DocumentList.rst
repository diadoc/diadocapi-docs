DocumentList
============

.. code-block:: protobuf

    message DocumentList {
        required int32 TotalCount = 1;
        repeated Document Documents = 2;
    }
        

Структура данных DocumentList представляет собой список документов, возвращаемый методом :doc:`../http/GetDocuments`. Поле DocumentList.TotalCount содержит общее количество документов, удовлетворяющих фильтру. Каждый элемент списка DocumentList.Documents представлен структурой :doc:`Document`.
