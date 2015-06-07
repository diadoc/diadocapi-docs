ForwardDocumentEvent
====================

.. code-block:: protobuf

    message ForwardDocumentEvent
    {
        optional Timestamp Timestamp = 1;
        optional string ToBoxId = 2;
    }
        

Структура данных ForwardDocumentEvent описывает событие пересылки документа третьей стороне:

-  Timestamp (всегда заполняется) - :doc:`метка времени <Timestamp>` события пересылки документа.

-  ToBoxId (всегда заполняется) - идентификатор ящика адресата пересылки (кому был передан документ).
