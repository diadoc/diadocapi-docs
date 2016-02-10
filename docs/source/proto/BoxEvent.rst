BoxEvent
========

.. code-block:: protobuf

    message BoxEvent {
        required string EventId = 1;
        optional Message Message = 2;
        optional MessagePatch Patch = 3;
    }
        

Структура данных BoxEvent представляет одно событие в ящике Диадока:

-  *EventId* - уникальный идентификатор события;

-  *Message* - структура типа :doc:`Message`, содержащая данные о событии, соответствующем появлению в ящике нового сообщения или черновика;

-  *Patch* - структура типа :doc:`MessagePatch`, содержащая данные о событии, соответствующем появлению дополнений к уже существующему в ящике сообщению или черновику.

В структуре *BoxEvent* одно и только одно из полей *Message* и *Patch* может быть отлично от NULL.