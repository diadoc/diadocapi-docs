Message
=======

.. code-block:: protobuf

    message Message {
        required string MessageId = 1;
        required sfixed64 TimestampTicks = 2;
        required sfixed64 LastPatchTimestampTicks = 3;
        required string FromBoxId = 4;
        required string FromTitle = 5;
        optional string ToBoxId = 6;
        optional string ToTitle = 7;
        repeated Entity Entities = 8;
        optional bool IsDraft = 9 [default = false];
        optional bool DraftIsLocked = 10 [default = false];
        optional bool DraftIsRecycled = 11 [default = false];
        optional string CreatedFromDraftId = 12;
        optional string DraftIsTransformedToMessageId = 13;
        optional bool IsDeleted = 14 [default = false];
        optional bool IsTest = 15 [default = false];
        optional bool IsInternal = 16 [default = false];
    }
        

Структура данных *Message* представляет одно сообщение или черновик в Диадоке:

-  *MessageId* - уникальный идентификатор сообщения или черновика;

-  *TimestampTicks* - :doc:`метка времени <Timestamp>` создания сообщения;

-  *LastPatchTimestampTicks* - :doc:`метка времени <Timestamp>` последнего патча (дополнения), примененного к данному сообщению;

-  *FromBoxId* - идентификатор ящика отправителя сообщения;

-  *ToBoxId* - идентификатор ящика получателя сообщения; в случае если данное сообщение является черновиком, данное поле может быть не заполнено;

-  *FromTitle* - человекочитаемое имя ящика отправителя сообщения;

-  *ToTitle* - человекочитаемое имя ящика получателя сообщения; в случае если данное сообщение является черновиком, данное поле может быть не заполнено;

-  *Entities* - список сущностей, составляющих данное сообщение (включая сущности из дополнений к нему); каждая сущность представлена структурой типа :doc:`Entity <Entity message>`;

-  *IsDraft* - флаг, показывающий, является ли данное сообщение черновиком;

-  *DraftIsLocked* - флаг, показывающий, что данный черновик заблокирован, то есть в него нельзя добавлять, или удалять из него документы. Такой черновик можно только либо отправить, превратив в полноценное сообщение, либо удалить; данное поле заполняется только в структурах Message, представляющих черновики;

-  *DraftIsRecycled* - флаг, показывающий, что данный черновик утилизирован, то есть он был либо удален, либо на его основе было создано полноценное сообщение и отправлено получателю; в последнем случае у этого черновика также заполнено поле *DraftIsTransformedToMessageId*, а у соответствующего сообщения заполнено поле *CreatedFromDraftId*; поле *DraftIsRecycled* заполняется только в структурах *Message*, представляющих черновики;

-  *CreatedFromDraftId* - идентификатор сообщения-черновика, на основе которого было создано данное сообщение; данное поле заполняется только у тех сообщений, которые формируются на основе черновиков;

-  *DraftIsTransformedToMessageId* - идентификатор сообщения, которое было создано на основе данного черновика; данное поле заполняется только в структурах Message, представляющих черновики;

-  *IsDeleted* - флаг, показывающий, было ли удалено данное сообщение;

-  *IsTest* - флаг, показывающий, что данное сообщение является тестовым и не имеет юридической силы;

-  *IsInternal* - флаг, показывающий, что данное сообщение является внутренним.