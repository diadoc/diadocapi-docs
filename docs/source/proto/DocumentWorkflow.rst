DocumentWorkflow
================

Представляет вид документооборота.

.. code-block:: protobuf

    message DocumentWorkflow {
        required int32 Id = 1;
        required bool IsDefault = 2;
    }

-  *Id* - уникальный числовой идентификатор вида документооборота
-  *IsDefault* - вид документооборота будет использован по умолчанию

.. Существуют следующие виды документооборота:
   (Здесь будет таблица)