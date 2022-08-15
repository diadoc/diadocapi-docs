GetDocflowsByPacketIdRequest
============================

Структура ``GetDocflowsByPacketIdRequest`` представляет собой запрос для получения документов методом :doc:`../http/GetDocflowsByPacketId`.

.. code-block:: protobuf

    message GetDocflowsByPacketIdRequest
    {
        required string PacketId = 1;
        optional int32 Count = 2 [default = 100];
        optional bool InjectEntityContent = 3 [default = false];
        optional bytes AfterIndexKey = 4;
    }

- ``PacketId`` — идентификатор пакета.
- ``Count`` — максимальное количество документов в выдаче, не должно превышать 100.
- ``InjectEntityContent`` — признак того, что в выдачу нужно включить содержимое документа.
- ``AfterIndexKey`` — индекс предыдущего документа, который не будет включен в запрашиваемую страницу. Используется для постраничного получения документов, если их количество в результате поиска превышает максимальное значение в 100 элементов.

----

.. rubric:: Смотри также

*Структура используется:*
	- в теле запроса метода :doc:`../http/GetDocflowsByPacketId`.