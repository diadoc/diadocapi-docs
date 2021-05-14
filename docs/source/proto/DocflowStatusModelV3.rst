DocflowStatusModelV3
==================

.. code-block:: protobuf

   message DocflowStatusModelV3
   {
       optional string Severity = 1;
       optional string StatusText = 2;
   }

Структура представляет компоненту статуса документооборота.

-  *Severity* - уровень критичность статуса, принимает одно из значений

  - *UnknownStatusSeverity*
  
  - *Info*
  
  - *Success*
  
  - *Warning*
  
  - *Error*
  
-  *StatusText* - основной текст описания статуса.
