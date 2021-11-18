DocflowStatusModel
==================

.. tip::
	Эта структура относится к устаревшей версии Docflow API. Мы рекомендуем использовать последнюю версию :doc:`Docflow API <../Docflow API>` — V3. В нее включена аналогичная структура :doc:`DocflowStatusModelV3`.

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

.. rubric:: Использование

Эта структура используется в структуре :doc:`DocflowStatus`.
