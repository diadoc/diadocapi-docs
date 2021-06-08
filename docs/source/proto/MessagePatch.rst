MessagePatch
============

.. code-block:: protobuf

    message MessagePatch {
        required string MessageId = 1;
        required sfixed64 TimestampTicks = 2;
        repeated Entity Entities = 3;
        optional bool ForDraft = 4 [default = false];
        optional bool DraftIsRecycled = 5 [default = false];
        repeated string DraftIsTransformedToMessageIdList = 6;
        optional bool DraftIsLocked = 7 [default = false];
        optional bool MessageIsDeleted = 8 [default = false];
        repeated EntityPatch EntityPatches = 9;
        optional bool MessageIsRestored = 10 [default = false];
        optional bool MessageIsDelivered = 11 [default = false];
        optional string DeliveredPatchId = 12;
        required string PatchId = 13;
        optional string NotDeliveredEventId = 14;
        required MessageType MessageType = 15;
    }

    message EntityPatch {
        required string EntityId = 1;
        optional bool DocumentIsDeleted = 2 [default = false];
        optional string MovedToDepartment = 3;
        optional bool DocumentIsRestored = 4 [default = false];
        optional bool ContentIsPatched = 5 [default = false];
        optional string ForwardedToBoxId = 6;
    }
        

Структура данных MessagePatch представляет дополнение (патч) к :doc:`сообщению <Message>` в Диадоке:

-  *MessageId* - идентификатор сообщения, к которому относится данный патч.

-  *TimestampTicks* - :doc:`метка времени <Timestamp>` создания патча.

-  *Entities* - список сущностей, составляющих данное дополнение к сообщению. Каждая сущность представлена структурой типа :doc:`Entity <Entity message>`.

-  *ForDraft* - флаг, показывающий, является ли сообщение, к которому относится данный патч, черновиком.

-  *DraftIsRecycled* - флаг, показывающий, что черновик, к которому относится данный патч, был утилизирован, то есть он был либо удален, либо на его основе было создано полноценное сообщение и отправлено получателю. Поле *DraftIsRecycled* заполняется только в патчах, относящихся к черновикам.

-  *DraftIsTransformedToMessageIdList* - идентификаторы сообщений, созданных на основе черновика, к которому относится данный патч. Поле DraftIsTransformedToMessageIdList заполняется только в патчах, относящихся к черновикам.

-  *DraftIsLocked* - флаг, показывающий, что черновик, к которому относится данный патч, был заблокирован. После этого в этот черновик нельзя добавлять, или удалять из него документы. Такой черновик можно только либо отправить, превратив в полноценное сообщение, либо удалить. Поле DraftIsLocked заполняется только в патчах, относящихся к черновикам.

-  *MessageIsDeleted* - флаг, показывающий, что сообщение, к которому относится данный патч, было удалено.

-  *EntityPatches* - список патчей к сущностям сообщения, к которому относится данный патч. Каждый такой патч представлен структурой типа EntityPatch.

-  *MessageIsRestored* - флаг, показывающий, что сообщение, к которому относится данный патч, было восстановлено из удаленных.

-  *MessageIsDelivered* - флаг, показывающий, что сообщение, к которому относится данный патч, было доставлено получателю.

-  *DeliveredPatchId* - идентификатор доставленного получателю патча.

-  *PatchId* - идентификатор патча.

-  *MessageType* - тип сообщения :doc:`../proto/MessageType`.

Структура данных *EntityPatch* представляет дополнение (патч) к :doc:`сущности <Entity message>` в Диадоке:

-  *EntityId* - идентификатор сущности, к которой относится данный патч.

-  *DocumentIsDeleted* - флаг, показывающий, что документ, к которому относится данный патч, был удален.

-  *MovedToDepartment* - поле заполняется в случае перемещения документа между подразделениями организации и содержит идентификатор подразделения, в которое был перемещен документ.

-  *DocumentIsRestored* - флаг, показывающий, что документ, к которому относится данный патч, был восстановлен из удаленных.

-  *ContentIsPatched* - флаг, показывающий, что исходящий документ, к которому относится данный патч, был подписан, а к содержимому документа были добавлены данные из сертификата подписанта.

-  *ForwardedToBoxId* - идентификатор ящика получателя при пересылке документа третьей стороне.
