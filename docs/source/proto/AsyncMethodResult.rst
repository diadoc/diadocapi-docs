AsyncMethodResult
=================

.. code-block:: protobuf

        message AsyncMethodResult {
            optional string TaskId = 1;
        }
        
-  ``TaskId`` — результат вызова асинхронного метода. Используется для получения конечного результата через вызов парного метода. 

----

.. rubric:: Смотри также

*Структура используется:*
	- в теле ответа парных методов :doc:`../http/CloudSign` и :doc:`../http/CloudSignResult`,
	- в теле ответа парных методов :doc:`../http/DssSign` и :doc:`../http/DssSignResult`,
	- в теле ответа парных методов :doc:`../http/RegisterPowerOfAttorney` и :doc:`../http/RegisterPowerOfAttorneyResult`.