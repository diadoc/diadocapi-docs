GetDocflowsByPacketIdRequest
============================

.. code-block:: protobuf

    message GetDocflowsByPacketIdRequest
    {
        required string PacketId = 1;
        optional int32 Count = 2 [default = 100];
        optional bool InjectEntityContent = 3 [default = false];
        optional bytes AfterIndexKey = 4;
    }

Структура представляет запрос, передаваемый методу :doc:`../http/GetDocflowsByPacketId`.

-  *PacketId* - идентификатор пакета.

-  *Count* - максимальное количество документов в выдаче, не должно превышать 100.

-  *InjectEntityContent* - признак того, что в выдачу нужно включить содержимое документа.

-  *AfterIndexKey* - ключ, использующийся для постраничной выгрузки. Ключу *AfterIndexKey* соответствует предыдущий документ, который в выдачу не попадает.
