MessagePatchToPost
==================

Структура ``MessagePatchToPost`` представляет собой дополнение к сообщению для отправки методом :doc:`../http/PostMessagePatch`.

.. code-block:: protobuf

    message MessagePatchToPost {
        required string BoxId = 1;
        required string MessageId = 2;
        repeated ReceiptAttachment Receipts = 3;
        repeated CorrectionRequestAttachment CorrectionRequests = 4;
        repeated DocumentSignature Signatures = 5;
        repeated RequestedSignatureRejection RequestedSignatureRejections = 6;  // Устаревшая структура
        repeated RecipientTitleAttachment XmlTorg12BuyerTitles = 7;
        repeated RecipientTitleAttachment XmlAcceptanceCertificateBuyerTitles = 8;
        repeated ResolutionAttachment Resolutions = 9;
        repeated ResolutionRequestAttachment ResolutionRequests = 10;
        repeated ResolutionRequestCancellationAttachment ResolutionRequestCancellations = 11;
        repeated ResolutionRequestDenialAttachment ResolutionRequestDenials = 12;
        repeated ResolutionRequestDenialCancellationAttachment ResolutionRequestDenialCancellations = 13;
        repeated RevocationRequestAttachment RevocationRequests = 14;
        repeated XmlSignatureRejectionAttachment XmlSignatureRejections = 15;
        repeated CustomDataPatch CustomDataPatches = 16;
        repeated ResolutionRouteAssignment ResolutionRouteAssignments = 17;
        repeated SignatureVerification SignatureVerifications = 18;
        repeated EditDocumentPacketCommand EditDocumentPacketCommands = 19;
        repeated RecipientTitleAttachment UniversalTransferDocumentBuyerTitles = 20;
        repeated ResolutionRouteRemoval ResolutionRouteRemovals = 21;
        repeated RecipientTitleAttachment RecipientTitles = 22; 
        repeated EditingPatch EditingPatches = 24;
    }

    message ReceiptAttachment {
        required string ParentEntityId = 1;
        required SignedContent SignedContent = 2;
        repeated string Labels = 4;
    }

    message CorrectionRequestAttachment {
        required string ParentEntityId = 1;
        required SignedContent SignedContent = 2;
        repeated string Labels = 4;
    }

    message RecipientTitleAttachment {
        required string ParentEntityId = 1;
        required SignedContent SignedContent = 2;
        repeated string Labels = 4;
        required bool NeedReceipt = 5 [default = false];
    }

    message RequestedSignatureRejection {
        required string ParentEntityId = 1;
        required SignedContent SignedContent = 2;
        repeated string Labels = 3;
    }

    message RevocationRequestAttachment {
        required string ParentEntityId = 1;
        required SignedContent SignedContent = 2;
        repeated string Labels = 3;
    }

    message XmlSignatureRejectionAttachment {
        required string ParentEntityId = 1;
        required SignedContent SignedContent = 2;
        repeated string Labels = 3;
    }

    message ResolutionRouteAssignment {
        required string InitialDocumentId = 1;
        required string RouteId = 2;
        optional string Comment = 3;
        repeated string Labels = 4;
    }

    message SignatureVerification {
        required string InitialDocumentId = 1;
        required bool IsValid = 2;
        optional string ErrorMessage = 3;
        repeated string Labels = 4;
    }

    message EditDocumentPacketCommand {
        required string DocumentId = 1;
        repeated DocumentId AddDocumentsToPacket = 2;
        repeated DocumentId RemoveDocumentsFromPacket = 3;
    }

    message ResolutionRouteRemoval {
        required string ParentEntityId = 1;
        required string RouteId = 2;
        optional string Comment = 3;
        repeated string Labels = 4;
    }

    message EditingPatch {
        required string ParentEntityId = 1;
        required UnsignedContent Content = 2;
        repeated string Labels = 3;
    }

- ``BoxId`` — идентификатор ящика организации, в котором находится исходное сообщение.

- ``MessageId`` — идентификатор сообщения, к которому относится дополнение.

- ``Receipts`` — список извещений о получении документов, подлежащих отправке и предусмотренных порядком обмена электронными счетами-фактурами. Представлены структурой ``ReceiptAttachment``. Структура представляет собой извещение о получении документа в отправляемом дополнении:

	- ``ParentEntityId`` — идентификатор документа, к которому относится извещение. Этот идентификатор принимает значение одной из :doc:`сущностей <Entity message>` родительского сообщения (поле ``EntityId``).

	- ``SignedContent`` — содержимое файла извещения вместе с электронной подписью, представленное структурой :doc:`SignedContent`.

	- ``Labels`` — список :doc:`меток <Labels>` извещения о получении.

- ``CorrectionRequests`` — список уведомлений об уточнении СФ/ИСФ/КСФ/ИКСФ, подлежащих отправке и предусмотренных порядком обмена электронными счетами-фактурами. Представлены структурой ``CorrectionRequestAttachment``. Структура представляет собой одно уведомление об уточнении СФ/ИСФ/КСФ/ИКСФ в отправляемом дополнении:

	- ``ParentEntityId`` — идентификатор СФ/ИСФ/КСФ/ИКСФ, к которому относится уведомление. Этот идентификатор принимает значение одной из :doc:`сущностей <Entity message>` родительского сообщения (поле ``EntityId``).

	- ``SignedContent`` — содержимое файла уведомления с электронной подписью, представленное структурой :doc:`SignedContent`.

	- ``Labels`` — список :doc:`меток <Labels>` уведомления об уточнении.

- ``Signatures`` — список подписей под документами, представленных структурой :doc:`DocumentSignature`. Могут быть:

	- подписями отправителя — для отправки документов, сохраненных без отправки,
	- подписями получателя — для двусторонних документов с запросом подписи,
	- согласующими подписями под документом,
	- ответными подписями под запросом на аннулирование документа.

- ``RequestedSignatureRejections`` — поле устарело, используйте ``XmlSignatureRejections``. Представлено структурой ``RequestedSignatureRejection``. Структура представляет собой один отказ в формировании запрошенной подписи:

	- ``ParentEntityId`` — идентификатор документа, к которому относится отказ. Этот идентификатор принимает значение одной из :doc:`сущностей <Entity message>` родительского сообщения (поле ``EntityId``).

	- ``SignedContent`` — текст причины отказа с электронной подписью, представленный структурой :doc:`SignedContent`. Текст причины отказа должен быть указан в поле ``SignedContent.Content`` в кодировке UTF-8.

	- ``Labels`` — список :doc:`меток <Labels>` отказа.

- ``XmlTorg12BuyerTitles`` — список титулов покупателя для товарных накладных ТОРГ-12 в XML-формате, подлежащих отправке. Рекомендуем вместо него заполнять поле ``RecipientTitles``.

- ``XmlAcceptanceCertificateBuyerTitles`` — список титулов заказчика для актов о выполнении работ или оказании услуг в XML-формате, подлежащих отправке. Рекомендуем вместо него заполнять поле ``RecipientTitles``.

- ``RecipientTitles`` — список титулов получателя для любого типа документов, подлежащих отправке. 

- ``Resolutions`` — список действий по согласованию к документам сообщения, к которому относится дополнение. Представлены структурой :doc:`ResolutionAttachment <Resolution>`.

- ``ResolutionRequests`` — список запросов на согласование или подпись документа, представленных структурой :doc:`ResolutionRequestAttachment <ResolutionRequest>`

- ``ResolutionRequestCancellations`` — список действий, отменяющих отправленные ранее запросы на согласование документа. Представлены структурой :doc:`ResolutionRequestCancellationAttachment <ResolutionRequest>`

- ``ResolutionRequestDenials`` — список действий по отказу от запроса подписи. Отказ аннулирует ошибочный отправленный запрос на подпись со стороны получателя запроса. Представлены структурой :doc:`ResolutionRequestDenialAttachment <ResolutionRequestDenial>`

- ``ResolutionRequestDenialCancellations`` — список действий, отменяющих отказы от запросов подписей. При выполнении действий исходные запросы на подпись восстанавливаются. Представлены структурой :doc:`ResolutionRequestDenialCancellationAttachment <ResolutionRequestDenial>`

- ``RevocationRequests`` — список предложений об аннулировании документов. Представлены структурой ``RevocationRequestAttachment`` с полями:

	- ``ParentEntityId`` — идентификатор документа, к которому относится предложение. Этот идентификатор принимает значение одной из :doc:`сущностей <Entity message>` родительского сообщения (поле ``EntityId``).

	- ``SignedContent`` — содержимое файла предложения с электронной подписью, представленное структурой :doc:`SignedContent`.

	- ``Labels`` — список :doc:`меток <Labels>` предложения об аннулировании.

- ``XmlSignatureRejections`` — список действий по отказу от предложений об аннулировании или отказу от подписи документов. Представлены структурой ``XmlSignatureRejectionAttachment``. Структура представляет собой  одно действие по отказу от предложения об аннулировании документа или по отказу от подписи документа:

	- ``ParentEntityId`` — идентификатор предложения об аннулировании или документа, к которому относится это действие. Этот идентификатор принимает значение одной из :doc:`сущностей <Entity message>` родительского сообщения (поле ``EntityId``).

	- ``SignedContent`` — содержимое файла отказа с электронной подписью, представленное структурой :doc:`SignedContent`.

	- ``Labels`` — список :doc:`меток <Labels>` отказа.

- ``CustomDataPatches`` — список операций по изменению пользовательских данных (:doc:`тегов <../entities/tag>`) у документов в исходном сообщении. Представлены структурой :doc:`CustomDataPatch`. Максимальное количество патчей — 15.

- ``EditDocumentPacketCommands`` — список операций по изменению состава пакета у документов в исходном сообщении. Представлены структурой ``EditDocumentPacketCommand``. Структура представляет собой действие по редактированию состава пакета одного из документов в сообщении:

	- ``DocumentId`` — идентификатор документа, пакет которого редактируется.

	- ``AddDocumentsToPacket`` — список идентификаторов документов, которые нужно добавить в пакет к заданному документу. Представлены структурой :doc:`DocumentId`. Каждый идентификатор должен соответствовать документу из ящика, в котором находится редактируемый документ. Если добавляемый документ является частью другого пакета, то в редактируемый пакет будут добавлены все документы из старого пакета — пакеты объединяются целиком. Если объединять пакеты не нужно, перед добавлением удалите лишние документы из старого пакета, используя поле ``RemoveDocumentsFromPacket``.

	- ``RemoveDocumentsFromPacket`` — список идентификаторов документов, которые нужно удалить из пакета заданного документа. Если в пакете есть документ с таким идентификатором, то он удалится из пакета и образует новый пакет из одного документа. Если такого документа нет, ничего не произойдет.

- ``UniversalTransferDocumentBuyerTitles`` — список титулов покупателя УПД. Рекомендуем вместо него заполнять поле ``RecipientTitles``.

- ``ResolutionRouteAssignments`` — список операций по постановке документов на маршрут согласования. Представлены структурой ``ResolutionRouteAssignment``. Структура представляет собой одно действие на постановку документа на маршрут согласования:

	- ``InitialDocumentId`` — идентификатор документа, который нужно поставить на маршрут согласования.

	- ``RouteId`` — идентификатор маршрута согласования, на который нужно поставить документ.

	- ``Comment`` — текстовый комментарий. Длина не должна превышать 500 символов.

	- ``Labels`` — список :doc:`меток <Labels>` постановки на маршрут.

- ``ResolutionRouteRemovals`` — список операций по снятию документов с маршрута согласования. Представлены структурой ``ResolutionRouteRemoval``. Структура представляет собой одно действие на снятие документа с маршрута согласования:

	- ``ParentEntityId`` — идентификатор документа, который нужно снять с маршрута согласования.

	- ``RouteId`` — идентификатор маршрута согласования, с которого нужно снять документ.

	- ``Comment`` — текстовый комментарий. Длина не должна превышать 500 символов.

	- ``Labels`` — список :doc:`меток <Labels>` снятия с маршрута.

- ``EditingPatches`` — список операций по редактированию контента документа. Редактировать можно только документы, для которых была указана :ref:`настройка редактирования <editing_settings>` ``EditingSettingId``.

----

.. rubric:: Смотри также

*Структура используется:*
	- в теле запроса метода :doc:`../http/PostMessagePatch`.