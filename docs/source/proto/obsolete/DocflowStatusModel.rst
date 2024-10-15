DocflowStatusModel
==================

.. warning::
	Структура устарела. Вместо нее используется структура :doc:`../DocflowStatusModelV3`.

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

.. rubric:: См. также

*Структура используется:*
	- в устаревшей структуре :doc:`DocflowStatus`
