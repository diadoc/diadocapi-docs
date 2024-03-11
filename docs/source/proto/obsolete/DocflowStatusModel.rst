DocflowStatusModel
==================

.. warning::
	Структура относится к устаревшей версии Docflow API. Используйте структуру :doc:`../../proto/DocflowStatusModelV3` последней версии :doc:`../../Docflow API` — V3.

.. code-block:: protobuf

    message DocflowStatusModel
    {
        optional Severity = 1 [default = UnknownDocflowStatusSeverity];
        optional string StatusText = 2;
        optional string StatusHint = 3;
    }

Структура представляет собой составную часть статуса документооборота.

- :doc:`Severity <DocflowStatusSeverity>` — уровень критичность статуса.

- ``StatusText`` — основной текст статуса.

- ``StatusHint`` — дополнительный текст статуса.

----

.. rubric:: Смотри также

*Структура используется:*
	- в структуре :doc:`DocflowStatus`.
