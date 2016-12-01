MessagePatchToPost
==================

.. code-block:: protobuf

    message MessagePatchToPost {
        required string BoxId = 1;
        required string MessageId = 2;
        repeated ReceiptAttachment Receipts = 3;
        repeated CorrectionRequestAttachment CorrectionRequests = 4;
        repeated DocumentSignature Signatures = 5;
        repeated RequestedSignatureRejection RequestedSignatureRejections = 6;
        repeated ReceiptAttachment XmlTorg12BuyerTitles = 7;
        repeated ReceiptAttachment XmlAcceptanceCertificateBuyerTitles = 8;
        repeated ResolutionAttachment Resolutions = 9;
        repeated ResolutionRequestAttachment ResolutionRequests = 10;
        repeated ResolutionRequestCancellationAttachment ResolutionRequestCancellations = 11;
        repeated ResolutionRequestDenialAttachment ResolutionRequestDenials = 12;
        repeated ResolutionRequestDenialCancellationAttachment ResolutionRequestDenialCancellations = 13;
        repeated RevocationRequestAttachment RevocationRequests = 14;
        repeated XmlSignatureRejectionAttachment XmlSignatureRejections = 15;
        repeated CustomDataPatch CustomDataPatches = 16;
        repeated ResolutionChainAssignment ResolutionChainAssignments = 17;
        repeated SignatureVerification SignatureVerifications = 18;
        repeated EditDocumentPacketCommand EditDocumentPacketCommands = 19;
        repeated ReceiptAttachment UniversalTransferDocumentBuyerTitles = 20;
    }

    message ReceiptAttachment {
        required string ParentEntityId = 1;
        required SignedContent SignedContent = 2;
    }

    message ResolutionChainAssignment {
        required string InitialDocumentId = 1;
        required string ChainId = 2;
        optional string Comment = 3;
    }

    message CorrectionRequestAttachment {
        required string ParentEntityId = 1;
        required SignedContent SignedContent = 2;
    }

    message RequestedSignatureRejection {
        required string ParentEntityId = 1;
        required SignedContent SignedContent = 2;
    }

    message RevocationRequestAttachment {
        required string ParentEntityId = 1;
        required SignedContent SignedContent = 2;
    }

    message XmlSignatureRejectionAttachment {
        required string ParentEntityId = 1;
        required SignedContent SignedContent = 2;
    }

    message SignatureVerification {
        required string InitialDocumentId = 1;
        required bool IsValid = 2;
        optional string ErrorMessage = 3;
    }

    message EditDocumentPacketCommand {
        required string DocumentId = 1;
        repeated DocumentId AddDocumentsToPacket = 2;
        repeated DocumentId RemoveDocumentsFromPacket = 3;
    }
        

Структура данных *MessagePatchToPost* представляет дополнение к сообщению, подлежащее отправке через Диадок при помощи метода :doc:`../http/PostMessagePatch`:

-  *BoxId* - идентификатор ящика, в котором находится исходное сообщение.

-  *MessageId* - идентификатор сообщения, к которому относится отправляемый патч.

-  *Receipts* - список подлежащих отправке извещений о получении различных документов, предусмотренных порядком обмена электронными счетами-фактурами.

-  *CorrectionRequests* - список подлежащих отправке уведомлений об уточнении СФ/ИСФ/КСФ/ИКСФ, предусмотренных порядком обмена электронными счетами-фактурами.

-  *Signatures* - список подписей под документами (см. описание структуры :doc:`DocumentSignature <DocumentSignature>`). Подписи могут быть подписями отправителя (для отправки документов, сохраненных без отправки), подписями получателя (для двусторонних документов с запросом подписи), согласующими подписями под документом, а также ответными подписями под запросом на аннулирование документа.

-  *RequestedSignatureRejections* - список отказов от запрошенных подписей под двусторонними документами.

-  *XmlTorg12BuyerTitles* - список подлежащих отправке титулов покупателя для товарных накладных ТОРГ-12 в XML-формате.

-  *XmlAcceptanceCertificateBuyerTitles* - список подлежащих отправке титулов заказчика для актов о выполнении работ (оказании услуг) в XML-формате.

-  *Resolutions* - список действий по согласованию к документам сообщения, к которому относится патч. Каждое действие является структурой :doc:`ResolutionAttachment <Resolution>`.

-  *ResolutionRequests* - список запросов на согласование (или подпись) документа. Каждый запрос представляется структурой :doc:`ResolutionRequestAttachment <ResolutionRequest>`

-  *ResolutionRequestCancellations* - список действий, отменяющих отправленные ранее запросы на согласование документа. Каждое действие представляется структурой :doc:`ResolutionRequestCancellationAttachment <ResolutionRequest>`

-  *ResolutionRequestDenials* - список действий по отказу от запроса подписи. Отказ предназначен для аннулирования (со стороны получателя запроса) ошибочного запроса на подпись, отправленного в рамках процесса согласования. Каждый отказ от запроса представляется структурой :doc:`ResolutionRequestDenialAttachment <ResolutionRequestDenial>`

-  *ResolutionRequestDenialCancellations* - список действий, отменяющих отказы от запросов подписей. При выполнении таких действий исходные запросы на подпись восстанавливаются. Каждое действие представляется структурой :doc:`ResolutionRequestDenialCancellationAttachment <ResolutionRequestDenial>`

-  *RevocationRequests* - список предложении об аннулировании документов. Каждое предложение представляется структурой *RevocationRequestAttachment*.

-  *XmlSignatureRejections* - список действий по отказу от предложений об аннулировании, а также действий по отказу от подписи документов. Каждый элемент представляется структурой *XmlSignatureRejectionAttachment*.

-  *CustomDataPatches* - список операций по изменению пользовательских данных у документов в исходном сообщении. Каждый элемент представляется структурой :doc:`CustomDataPatch <CustomDataPatch>`.

-  *EditDocumentPacketCommands* - список операций по изменению состава пакета у документов в исходном сообщении. Каждый элемент представляется структурой *EditDocumentPacketCommand*.

Структура данных *ReceiptAttachment* представляет одно извещение о получении документа в отправляемом патче:

-  *ParentEntityId* - идентификатор документа, к которому относится данное извещение. Это идентификатор соответствующей сущности из родительского сообщения (поле EntityId в структуре :doc:`Entity <Entity message>`).

-  *SignedContent* - содержимое файла извещения вместе с ЭЦП под ним в виде структуры :doc:`SignedContent`. В случае *ReceiptAttachment* поле *SignedContent.SignByAttorney* не может быть равно true (подпись "по доверенности" под извещениями о получении документов запрашивать нельзя).

Структура данных *CorrectionRequestAttachment* представляет одно уведомление об уточнении СФ/ИСФ/КСФ/ИКСФ в отправляемом патче:

-  *ParentEntityId* - идентификатор СФ/ИСФ/КСФ/ИКСФ, к которому относится данное уведомление. Это идентификатор соответствующей сущности из родительского сообщения (поле EntityId в структуре :doc:`Entity <Entity message>`).

-  *SignedContent* - содержимое файла уведомления вместе с ЭЦП под ним в виде структуры :doc:`SignedContent`.

Структура данных *RequestedSignatureRejection* представляет один отказ в формировании запрошенной подписи:

-  *ParentEntityId* - идентификатор документа, к которому относится данный отказ. Это идентификатор соответствующей сущности из родительского сообщения (поле EntityId в структуре :doc:`Entity <Entity message>`).

-  *SignedContent* - текст причины отказа вместе с ЭЦП под ним в виде структуры :doc:`SignedContent`. Текст причины отказа должен быть записан в поле SignedContent.Content в кодировке UTF-8.

Структура данных *RevocationRequestAttachment* представляет одно предложение об аннулировании документа в отправляемом патче:

-  *ParentEntityId* - идентификатор документа, к которому относится данное предложение. Это идентификатор соответствующей сущности из родительского сообщения (поле EntityId в структуре :doc:`Entity <Entity message>`).

-  *SignedContent* - содержимое файла предложения об аннулировании вместе с ЭЦП под ним в виде структуры :doc:`SignedContent`.

Структура данных *XmlSignatureRejectionAttachment* представляет одно действие по отказу от предложения об аннулировании документа, либо по отказу от подписи документа:

-  *ParentEntityId* - идентификатор предложения об аннулировании, либо документа, к которому относится данное действие. Это идентификатор соответствующей сущности из родительского сообщения (поле EntityId в структуре :doc:`Entity <Entity message>`).

-  *SignedContent* - содержимое файла отказа вместе с ЭЦП под ним в виде структуры :doc:`SignedContent`.

Структура *ResolutionChainAssignment* представляет одно действие на постановку документа на цепочку согласования:

-   *InitialDocumentId* - идентификатор документа, который нужно поставить на цепочку согласования;

-   *ChainId* - идентификатор цепочки согласования, на которую нужно поставить документ;

-   *Comment* - текстовый комментарий;

Структура *SignatureVerification* представляет собой результат проверки подписи на стороне получателя зашифрованного документа. Нужна для того, чтобы сообщить результат проверки подписи для зашифрованных документов:

-  *InitialDocumentId* - идентификатор документа

-  *IsValid* - флаг, показывающий результат проверки подписи на валидность,

-  *ErrorMessage* - текст ошибки, в случае если подпись не валидна

Структура данных *EditDocumentPacketCommand* представляет собой действие по редактированию состава пакета одного из документов в сообщении:

-  *DocumentId* - идентификатор документа, пакет которого редактируется,

-  *AddDocumentsToPacket* - список идентификаторов документов, которые нужно добавить в пакет к заданному документу. Каждый идентификатор представляется структурой :doc:`DocumentId <DocumentId>`. Каждый идентификатор должен соответствовать некоторому документу, уже существующему в том же ящике, что и редактируемый документ. Если добавляемый документ уже является частью другого пакета, то в редактируемый пакет вместе с добавляемым документом попадут и все остальные документы из его старого пакета, то есть пакеты объединяются целиком. Если такое поведение нежелательно, то необходимо предварительно удалить из второго пакета лишние документы при помощи RemoveDocumentsFromPacket (см. ниже).

-  *RemoveDocumentsFromPacket* - список идентификаторов документов, которые нужно удалить из пакета заданного документа. Если в пакете существует документ с таким идентификатором, то он удаляется из пакета и образует новый пакет, состоящий из одного документа. Если в пакете нет документа с таким идентификатором (например, он уже является частью другого пакета), то ничего не происходит.

- *UniversalTransferDocumentBuyerTitles* - список титулов покупателя УПД.