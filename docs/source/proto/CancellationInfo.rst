CancellationInfo
================

Структура ``CancellationInfo`` хранит информацию об отмене сущности.

.. code-block:: protobuf

   message CancellationInfo {
      required string Author = 1;
   }

- ``Author`` - ФИО сотрудника, выполнившего отмену.


----

.. rubric:: См. также

*Структура используется:*
	- в структуре :doc:`Entity message`