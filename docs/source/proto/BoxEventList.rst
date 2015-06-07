BoxEventList
============

.. code-block:: protobuf

    message BoxEventList {
        repeated BoxEvent Events = 1;
        optional int32 TotalCount = 2;
    }
        

Структура данных *BoxEventList* представляет собой список событий :doc:`BoxEvent`, возвращаемый методом :doc:`../http/GetNewEvents`. 

Поле *BoxEventList.TotalCount* содержит общее количество событий, удовлетворяющих запросу.
