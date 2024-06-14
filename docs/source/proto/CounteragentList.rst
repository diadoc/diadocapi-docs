CounteragentList
================

Структура ``CounteragentList`` представляет собой список контрагентов.

.. code-block:: protobuf

    message CounteragentList {
        required int32 TotalCount = 1;
        repeated Counteragent Counteragents = 2;
        required TotalCountType TotalCountType = 3;
    }

- ``TotalCount`` — количество контрагентов, удовлетворяющих запросу.
- ``Counteragents`` — список контрагентов. Каждый элемент списка представлен структурой :doc:`Counteragent`.
- ``TotalCountType`` — параметр, указывающий, является ли значение ``TotalCount`` точным или подсчет был ограничен максимальным количеством элементов в списке. Принимает значения из перечисления :doc:`TotalCountType`.

----

.. rubric:: См. также

*Структура используется:*
	- в теле ответа метода :doc:`../http/GetCounteragents`

*Определение:*
	- :doc:`../entities/counteragent`

*Руководства:*
	- :doc:`../instructions/counteragents`