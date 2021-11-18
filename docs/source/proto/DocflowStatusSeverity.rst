DocflowStatusSeverity
=====================

.. tip::
	Этот параметр относится к устаревшей версии Docflow API. Мы рекомендуем использовать последнюю версию :doc:`Docflow API <../Docflow API>` — V3.

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

.. rubric:: Использование

Этот параметр используется в структуре :doc:`DocflowStatusModel`.
