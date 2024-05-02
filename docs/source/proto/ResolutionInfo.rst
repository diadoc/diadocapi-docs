ResolutionInfo
==============

Структура ``ResolutionInfo`` содержит информацию о состоянии согласования.

.. code-block:: protobuf

    message ResolutionInfo {
        optional ResolutionType ResolutionType = 1 [default = UnknownResolutionType];
        required string Author = 2;
        optional string InitialRequestId = 3;
    }

- ``ResolutionType`` — тип действия по согласованию, принимает значения из перечисления :doc:`ResolutionType`.
- ``Author`` — ФИО пользователя, согласовавшего или отказавшего в согласовании.
- ``InitialRequestId`` — идентификатор запроса, в ответ на который сформировано согласование.

----

.. rubric:: См. также

*Структура используется:*
	- в структуре :doc:`Entity message`