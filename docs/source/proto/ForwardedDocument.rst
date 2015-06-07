ForwardedDocument
=================

.. code-block:: protobuf

    message ForwardedDocumentId
    {
        optional string FromBoxId = 1;
        optional DocumentId DocumentId = 2;
        optional string ForwardEventId = 3;
    }

    message ForwardedDocument
    {
        optional Timestamp ForwardTimestamp = 1;
        optional ForwardedDocumentId ForwardedDocumentId = 2;
        optional Docflow.DocumentWithDocflow DocumentWithDocflow = 3;
    }

Структура данных ForwardedDocument описывает переданный третьей стороне документ (по сути снэпшот состояния документа на момент пересылки):

-  *ForwardTimestamp* (всегда заполняется) - :doc:`метка времени <Timestamp>` события пересылки документа, которое привело к формированию данного пересланного документа.

-  *ForwardedDocumentId* (всегда заполняется) - идентификатор переданного третьей стороне документа.

-  *DocumentWithDocflow* (всегда заполняется) - состояние документа на момент пересылки.

Структура данных *ForwardedDocumentId* описывает идентификатор документа, переданного третьей стороне:

-  *FromBoxId* (всегда заполняется) - идентификатор ящика отправителя, инициировавшего пересылку.

-  *DocumentId* (всегда заполняется) - идентификатор документа в виде структуры :doc:`DocumentId`.

-  *ForwardEventId* (всегда заполняется) - уникальный идентификатор события пересылки документа.
