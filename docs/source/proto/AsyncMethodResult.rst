AsyncMethodResult
=================

.. code-block:: protobuf

        message AsyncMethodResult {
            optional string TaskId = 1;
        }
        
-  ``TaskId`` — результат вызова асинхронного метода. Используется для получения конечного результата через вызов парного метода. 

----

.. rubric:: Использование

Структура ``AsyncMethodResult`` используется в теле ответа парных методов:

- :doc:`../http/CloudSign` и :doc:`../http/CloudSignResult`
- :doc:`../http/DssSign` и :doc:`../http/DssSignResult`
- :doc:`../http/RegisterPowerOfAttorney` и :doc:`../http/RegisterPowerOfAttorneyResult`
