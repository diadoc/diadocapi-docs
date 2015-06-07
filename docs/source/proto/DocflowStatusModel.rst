DocflowStatusModel
==================

.. code-block:: protobuf

   message DocflowStatusModel
   {
       optional Severity = 1 [default = UnknownDocflowStatusSeverity];
       optional string StatusText = 2;
       optional string StatusHint = 3;
   }

Структура представляет компоненту статуса документооборота.

-  :doc:`Severity <DocflowStatusSeverity>` - уровень критичность статуса.

-  *StatusText* - основной текст описания статуса.

-  *StatusHint* - дополнительный текст статуса.
