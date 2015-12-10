AsyncMethodResult
=================

.. code-block:: protobuf

        message AsyncMethodResult {
            optional string TaskId = 1;
        }
        

-  *TaskId* - результат вызова асинхронного метода; используется для получения конечного результата через вызов другого, парного метода. 

Пример таких пар методов: :doc:`../http/CloudSign` и :doc:`../http/CloudSignResult`.