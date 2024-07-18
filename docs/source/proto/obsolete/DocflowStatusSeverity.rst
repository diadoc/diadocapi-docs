DocflowStatusSeverity
=====================

.. warning::
	Структура используется внутри устаревшей структуры :doc:`DocflowStatusModel`.

.. code-block:: protobuf

    enum DocflowStatusSeverity
    {
        UnknownDocflowStatusSeverity = 0;
        Info = 1;
        Success = 2;
        Warning = 3;
        Error = 4;
    }

Возможные уровни критичности статуса документа.

----

.. rubric:: См. также

*Перечисление используется:*
	- в структуре :doc:`DocflowStatusModel`
