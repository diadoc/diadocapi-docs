AsyncMethodResult
=================

.. code-block:: protobuf

    message AsyncMethodResult {
        optional string TaskId = 1;
    }

-  ``TaskId`` — результат вызова асинхронного метода. Используется для получения конечного результата через вызов парного метода. 


----

.. rubric:: См. также

*Структура используется:*
	- в теле ответа парных методов:

	  - :doc:`../http/AcquireCounteragent` и :doc:`../http/AcquireCounteragentResult`
	  - :doc:`../http/DssSign` и :doc:`../http/DssSignResult`
	  - :doc:`../http/RegisterPowerOfAttorney` и :doc:`../http/RegisterPowerOfAttorneyResult`