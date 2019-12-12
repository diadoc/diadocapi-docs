BoxEventList
============

.. code-block:: protobuf

    message BoxEventList {
        repeated BoxEvent Events = 1;
        optional int32 TotalCount = 2;
        required TotalCountType TotalCountType = 3;
    }
        

Структура данных *BoxEventList* представляет собой список событий :doc:`BoxEvent`, возвращаемый методом :doc:`../http/GetNewEvents`. 

Поле *BoxEventList.TotalCount* содержит количество событий, удовлетворяющих запросу. Поле *BoxEventList.TotalCountType* типа :doc:`TotalCountType` указывает, точно ли посчитан *TotalCount* или подсчет был ограничен после соответствующего значения.
