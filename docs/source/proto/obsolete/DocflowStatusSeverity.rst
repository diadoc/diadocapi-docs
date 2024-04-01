DocflowStatusSeverity
=====================

.. warning::
	Перечисление относится к устаревшей версии Docflow API. Используйте последнюю версию :doc:`../../Docflow API` — V3.

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
	- в структуре :doc:`DocflowStatusModel`.
