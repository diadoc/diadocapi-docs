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
        repeated string DraftIsTransformedToMessageIdList = 13;
        optional bool IsDeleted = 14 [default = false];
        optional bool IsTest = 15 [default = false];
        optional bool IsInternal = 16 [default = false];
        optional bool IsProxified = 17 [default = false];
        optional string ProxyBoxId = 18;
        optional string ProxyTitle = 19;
        optional bool PacketIsLocked = 20 [default = false];
        required LockMode LockMode = 21;
        required MessageType MessageType = 22;
        optional TemplateToLetterTransformationInfo TemplateToLetterTransformationInfo = 23;
        optional bool IsReusable = 24 [default = false];
    }


Структура данных *Message* представляет одно сообщение или черновик в Диадоке:

-  *MessageId* - уникальный идентификатор сообщения или черновика.

-  *TimestampTicks* - :doc:`метка времени <Timestamp>` создания сообщения.

-  *LastPatchTimestampTicks* - :doc:`метка времени <Timestamp>` последнего патча (дополнения), примененного к данному сообщению.

-  *FromBoxId* - идентификатор ящика отправителя сообщения.

-  *ToBoxId* - идентификатор ящика получателя сообщения. В случае если данное сообщение является черновиком, данное поле может быть не заполнено.

-  *FromTitle* - человекочитаемое имя ящика отправителя сообщения.

-  *ToTitle* - человекочитаемое имя ящика получателя сообщения. В случае если данное сообщение является черновиком, данное поле может быть не заполнено.

-  *Entities* - список сущностей, составляющих данное сообщение (включая сущности из дополнений к нему). Каждая сущность представлена структурой типа :doc:`Entity <Entity message>`.

-  *IsDraft* - флаг, показывающий, является ли данное сообщение черновиком (устаревшее, см. :doc:`MessageType`).

-  *DraftIsLocked* - флаг, показывающий, что данный черновик заблокирован, то есть в него нельзя добавлять, или удалять из него документы. Такой черновик можно только либо отправить, превратив в полноценное сообщение, либо удалить. Данное поле заполняется только в структурах Message, представляющих черновики.

-  *DraftIsRecycled* - флаг, показывающий, что данный черновик утилизирован, то есть он был либо удален, либо на его основе было создано полноценное сообщение и отправлено получателю. В последнем случае у этого черновика также заполнено поле *DraftIsTransformedToMessageId*, а у соответствующего сообщения заполнено поле *CreatedFromDraftId*. Поле *DraftIsRecycled* заполняется только в структурах *Message*, представляющих черновики.

-  *CreatedFromDraftId* - идентификатор сообщения-черновика, на основе которого было создано данное сообщение. Данное поле заполняется только у тех сообщений, которые формируются на основе черновиков.

-  *DraftIsTransformedToMessageIdList* - идентификатор сообщения, которое было создано на основе данного черновика. Данное поле заполняется только в структурах Message, представляющих черновики.

-  *IsDeleted* - флаг, показывающий, было ли удалено данное сообщение.

-  *IsTest* - флаг, показывающий, что данное сообщение является тестовым и не имеет юридической силы.

-  *IsInternal* - флаг, показывающий, что данное сообщение является внутренним.

-  *IsProxified* - флаг, показывающий отправлен ли документ через промежуточного получателя.

-  *ProxyBoxId* - идентификатор ящика, промежуточного получателя. Если указан ящик промежуточного получателя, то документ доставится конечному получателя только после того, как промежуточный получатель поставит подпись под документом. Если промежуточный получатель отклонит документ, то в ящик конечного получателя он не будет доставлен.

-  *ProxyTitle* - название организации промежуточного получателя.

-  *PacketIsLocked* - признак закрытого пакета. В таком пакете операция применяется ко всем документам сразу. Например, при подписании одного документа, подписываются сразу все.

-  *LockMode* - режим блокировки сообщения. Виды доступных режимы доступны в описании :doc:`../proto/LockMode`.

-  *MessageType* - тип сообщения :doc:`../proto/MessageType`.

-  *TemplateToLetterTransformationInfo* - содержит информацию о документе, который уже создан или будет создан на основе шаблона :doc:`../proto/TemplateToLetterTransformationInfo`.

-  *IsReusable* - флаг, показывающий, что сообщение создано на основе многоразового шаблона.