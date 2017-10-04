DocumentWorkflow
========================

.. code-block:: protobuf

    message DocumentWorkflow {
        required int32 Id = 1;
        required bool IsDefault = 2;
    }

Структура *DocumentWorkflow* представляет вид документооборота.

-  *Id* - уникальный числовой идентификатор вида документооборота
-  *IsDefault* - вид документооборот будет использован по умолчанию

Существуют следующие виды документооборота:

*Здесь таблицу*