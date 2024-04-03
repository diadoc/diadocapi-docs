MessagePatchToPost
==================

На этой странице описаны следующие структуры:

.. contents:: :local:


Структура ``MessagePatchToPost`` представляет собой дополнение к сообщению для отправки методом :doc:`../http/PostMessagePatch`.

.. code-block:: protobuf

    message MessagePatchToPost {
        required string BoxId = 1;
        required string MessageId = 2;
        repeated ReceiptAttachment Receipts = 3;
        repeated CorrectionRequestAttachment CorrectionRequests = 4;
        repeated DocumentSignature Signatures = 5;
        repeated RequestedSignatureRejection RequestedSignatureRejections = 6;
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
	
..

- ``BoxId`` — идентификатор ящика организации, в котором находится исходное сообщение.

- ``MessageId`` — идентификатор сообщения, к которому относится дополнение.

- ``Receipts`` — список извещений о получении документов, подлежащих отправке и предусмотренных порядком обмена электронными счетами-фактурами. Каждый элемент списка представлен структурой :ref:`ReceiptAttachment`.

- ``CorrectionRequests`` — список уведомлений об уточнении СФ/ИСФ/КСФ/ИКСФ, подлежащих отправке и предусмотренных порядком обмена электронными счетами-фактурами. Каждый элемент списка представлен структурой :ref:`CorrectionRequestAttachment`.

- ``Signatures`` — список подписей под документами, представленных структурой :doc:`DocumentSignature`. Подписи могут быть:

	- подписями отправителя — для отправки документов, сохраненных без отправки,
	- подписями получателя — для двусторонних документов с запросом подписи,
	- согласующими подписями под документом,
	- ответными подписями под запросом на аннулирование документа.

- ``RequestedSignatureRejections`` — список отказов в формировании запрошенной подписи. Каждый элемент списка представлен структурой :ref:`RequestedSignatureRejection`. Поле устарело, вместо него используйте поле ``XmlSignatureRejections``.

- ``XmlTorg12BuyerTitles`` — список титулов покупателя для товарных накладных ТОРГ-12 в XML-формате, подлежащих отправке. Каждый элемент списка представлен структурой :ref:`RecipientTitleAttachment`. Поле устарело, вместо него используйте поле ``RecipientTitles``.

- ``XmlAcceptanceCertificateBuyerTitles`` — список титулов заказчика для актов о выполнении работ или оказании услуг в XML-формате, подлежащих отправке. Каждый элемент списка представлен структурой :ref:`RecipientTitleAttachment`. Поле устарело, вместо него используйте поле ``RecipientTitles``.

- ``Resolutions`` — список действий по согласованию к документам сообщения, к которому относится дополнение. Каждый элемент списка представлен структурой :doc:`ResolutionAttachment <Resolution>`.

- ``ResolutionRequests`` — список запросов на согласование или подпись документа. Каждый элемент списка представлен структурой :doc:`ResolutionRequestAttachment <ResolutionRequest>`.

- ``ResolutionRequestCancellations`` — список действий, отменяющих отправленные ранее запросы на согласование документа. Каждый элемент списка представлен структурой :doc:`ResolutionRequestCancellationAttachment <ResolutionRequest>`.

- ``ResolutionRequestDenials`` — список действий по отказу от запроса подписи. Отказ аннулирует ошибочный отправленный запрос на подпись со стороны получателя запроса. Каждый элемент списка представлен структурой :doc:`ResolutionRequestDenialAttachment <ResolutionRequestDenial>`.

- ``ResolutionRequestDenialCancellations`` — список действий, отменяющих отказы от запросов подписей. При выполнении действий исходные запросы на подпись восстанавливаются. Каждый элемент списка представлен структурой :doc:`ResolutionRequestDenialCancellationAttachment <ResolutionRequestDenial>`.

- ``RevocationRequests`` — список предложений об аннулировании документов. Каждый элемент списка представлен структурой :ref:`RevocationRequestAttachment`.

- ``XmlSignatureRejections`` — список действий по отказу от предложений об аннулировании или отказу от подписи документов. Каждый элемент списка представлен структурой :ref:`XmlSignatureRejectionAttachment`.

- ``CustomDataPatches`` — список операций по изменению :doc:`пользовательских данных <../entities/tag>` документов в исходном сообщении. Каждый элемент списка представлен структурой :doc:`CustomDataPatch`. Максимальное количество патчей — 15.

- ``ResolutionRouteAssignments`` — список операций по постановке документов на маршрут согласования. Каждый элемент списка представлен структурой :ref:`ResolutionRouteAssignment`. 

- ``SignatureVerifications`` — список результатов проверки подписей зашифрованных документов на стороне получателя. Каждый элемент списка представлен структурой :ref:`SignatureVerification`.

- ``EditDocumentPacketCommands`` — список операций по изменению состава пакета у документов в исходном сообщении. Каждый элемент списка представлен структурой :ref:`EditDocumentPacketCommand`. 

- ``UniversalTransferDocumentBuyerTitles`` — список титулов покупателя УПД. Каждый элемент списка представлен структурой :ref:`RecipientTitleAttachment`. Поле устарело, вместо него используйте поле ``RecipientTitles``.

- ``ResolutionRouteRemovals`` — список операций по снятию документов с маршрута согласования. Каждый элемент списка представлен структурой :ref:`ResolutionRouteRemoval`.

- ``RecipientTitles`` — список титулов получателя для любого типа документов, подлежащих отправке. Каждый элемент списка представлен структурой :ref:`RecipientTitleAttachment`.

- ``EditingPatches`` — список операций по редактированию контента документа. Каждый элемент списка представлен структурой :ref:`EditingPatch`. Редактировать можно только документы, для которых была указана :ref:`настройка редактирования <editing_settings>` ``EditingSettingId``.


.. _ReceiptAttachment:

ReceiptAttachment
-----------------

Структура ``ReceiptAttachment`` представляет собой извещение о получении документа в отправляемом дополнении.

.. code-block:: protobuf

    message ReceiptAttachment {
        required string ParentEntityId = 1;
        required SignedContent SignedContent = 2;
        repeated string Labels = 4;
    }

..

- ``ParentEntityId`` — идентификатор документа, к которому относится извещение. Принимает значение одной из :doc:`сущностей <Entity message>` родительского сообщения (поле ``EntityId``).
- ``SignedContent`` — содержимое файла извещения вместе с электронной подписью, представленное структурой :doc:`SignedContent`.
- ``Labels`` — список :doc:`меток <Labels>`.


.. _CorrectionRequestAttachment:

CorrectionRequestAttachment
---------------------------

Структура ``CorrectionRequestAttachment`` представляет собой уведомление об уточнении СФ/ИСФ/КСФ/ИКСФ в отправляемом дополнении.

.. code-block:: protobuf

    message CorrectionRequestAttachment {
        required string ParentEntityId = 1;
        required SignedContent SignedContent = 2;
        repeated string Labels = 4;
    }

..

- ``ParentEntityId`` — идентификатор СФ/ИСФ/КСФ/ИКСФ, к которому относится уведомление. Принимает значение одной из :doc:`сущностей <Entity message>` родительского сообщения (поле ``EntityId``).
- ``SignedContent`` — содержимое файла уведомления с электронной подписью, представленное структурой :doc:`SignedContent`.
- ``Labels`` — список :doc:`меток <Labels>`.


.. _RequestedSignatureRejection:

RequestedSignatureRejection
---------------------------

Структура ``RequestedSignatureRejection`` представляет собой отказ в формировании запрошенной подписи.

.. code-block:: protobuf

    message RequestedSignatureRejection {
        required string ParentEntityId = 1;
        required SignedContent SignedContent = 2;
        repeated string Labels = 3;
    }

..

- ``ParentEntityId`` — идентификатор документа, к которому относится отказ. Принимает значение одной из :doc:`сущностей <Entity message>` родительского сообщения (поле ``EntityId``).
- ``SignedContent`` — причина отказа с электронной подписью, представленный структурой :doc:`SignedContent`. Текст причины отказа должен быть указан в поле ``SignedContent.Content`` в кодировке UTF-8.
- ``Labels`` — список :doc:`меток <Labels>`.


.. _RecipientTitleAttachment:

RecipientTitleAttachment
------------------------

Структура ``RecipientTitleAttachment`` представляет собой титул получателя любого типа документа.

.. code-block:: protobuf

    message RecipientTitleAttachment {
        required string ParentEntityId = 1;
        required SignedContent SignedContent = 2;
        repeated string Labels = 4;
        required bool NeedReceipt = 5 [default = false];
    }

..

- ``ParentEntityId`` — идентификатор титула исполнителя. Принимает значение одной из :doc:`сущностей <Entity message>` родительского сообщения (поле ``EntityId``).
- ``SignedContent`` — содержимое XML-файла титула с электронной подписью, представленное структурой :doc:`SignedContent`.
- ``Labels`` — список :doc:`меток <Labels>`.
- ``NeedReceipt`` — необязательный признак того, что от получателя требуется сформировать извещение о получении данного документа.


.. _RevocationRequestAttachment:

RevocationRequestAttachment
---------------------------

Структура ``RevocationRequestAttachment`` представляет собой предложение об аннулировании документа.

.. code-block:: protobuf

    message RevocationRequestAttachment {
        required string ParentEntityId = 1;
        required SignedContent SignedContent = 2;
        repeated string Labels = 3;
    }

..

- ``ParentEntityId`` — идентификатор документа, к которому относится предложение. Принимает значение одной из :doc:`сущностей <Entity message>` родительского сообщения (поле ``EntityId``).
- ``SignedContent`` — содержимое файла предложения с электронной подписью, представленное структурой :doc:`SignedContent`.
- ``Labels`` — список :doc:`меток <Labels>`.


.. _XmlSignatureRejectionAttachment:

XmlSignatureRejectionAttachment
-------------------------------

Структура ``XmlSignatureRejectionAttachment`` представляет собой действие по отказу от предложения об аннулировании документа или по отказу от подписи документа.

.. code-block:: protobuf

    message XmlSignatureRejectionAttachment {
        required string ParentEntityId = 1;
        required SignedContent SignedContent = 2;
        repeated string Labels = 3;
    }

..

- ``ParentEntityId`` — идентификатор предложения об аннулировании или документа, к которому относится это действие. Принимает значение одной из :doc:`сущностей <Entity message>` родительского сообщения (поле ``EntityId``).
- ``SignedContent`` — содержимое файла отказа с электронной подписью, представленное структурой :doc:`SignedContent`.
- ``Labels`` — список :doc:`меток <Labels>`.


.. _ResolutionRouteAssignment:

ResolutionRouteAssignment
-------------------------

Структура ``ResolutionRouteAssignment`` представляет собой действие по постановке документа на маршрут согласования.

.. code-block:: protobuf

    message ResolutionRouteAssignment {
        required string InitialDocumentId = 1;
        required string RouteId = 2;
        optional string Comment = 3;
        repeated string Labels = 4;
    }

..

- ``InitialDocumentId`` — идентификатор документа, который нужно поставить на маршрут согласования.
- ``RouteId`` — идентификатор маршрута согласования, на который нужно поставить документ.
- ``Comment`` — текстовый комментарий. Длина не должна превышать 500 символов.
- ``Labels`` — список :doc:`меток <Labels>`.


.. _SignatureVerification:

SignatureVerification
---------------------

Структура ``SignatureVerification`` представляет собой результат проверки подписей зашифрованного документа на стороне получателя.

Получатель с помощью метода :doc:`../http/GetCounteragentCertificates` может получить сертификаты отправителя документа, а затем с их помощью проверить подписи документа. Результаты  такой проверки можно внести в структуру ``SignatureVerification``.

.. code-block:: protobuf

    message SignatureVerification {
        required string InitialDocumentId = 1;
        required bool IsValid = 2;
        optional string ErrorMessage = 3;
        repeated string Labels = 4;
    }

..

- ``InitialDocumentId`` —  идентификатор проверяемого зашифрованного документа.
- ``IsValid`` — результат проверки документа.
- ``ErrorMessage`` — текст с описанием результата проверки.
- ``Labels`` — список :doc:`меток <Labels>`.


.. _EditDocumentPacketCommand:

EditDocumentPacketCommand
-------------------------

Структура ``EditDocumentPacketCommand`` представляет собой действие по редактированию состава пакета одного из документов в сообщении.

.. code-block:: protobuf

    message EditDocumentPacketCommand {
        required string DocumentId = 1;
        repeated DocumentId AddDocumentsToPacket = 2;
        repeated DocumentId RemoveDocumentsFromPacket = 3;
    }

..

- ``DocumentId`` — идентификатор документа, пакет которого редактируется.

- ``AddDocumentsToPacket`` — список идентификаторов документов, которые нужно добавить в пакет к заданному документу. Каждый элемент списка представлен структурой :doc:`DocumentId`.

 Каждый идентификатор должен соответствовать документу из ящика, в котором находится редактируемый документ. Если добавляемый документ является частью другого пакета, то в редактируемый пакет будут добавлены все документы из старого пакета — пакеты объединяются целиком. Если объединять пакеты не нужно, перед добавлением удалите лишние документы из старого пакета, используя поле ``RemoveDocumentsFromPacket``.

- ``RemoveDocumentsFromPacket`` — список идентификаторов документов, которые нужно удалить из пакета заданного документа. Каждый элемент списка представлен структурой :doc:`DocumentId`.

 Если в пакете есть документ с таким идентификатором, то он удалится из пакета и образует новый пакет из одного документа. Если такого документа нет, ничего не произойдет.


.. _ResolutionRouteRemoval:

ResolutionRouteRemoval
----------------------

Структура ``ResolutionRouteRemoval`` представляет собой действие по снятию документа с маршрута согласования.

.. code-block:: protobuf

    message ResolutionRouteRemoval {
        required string ParentEntityId = 1;
        required string RouteId = 2;
        optional string Comment = 3;
        repeated string Labels = 4;
    }

..

- ``ParentEntityId`` — идентификатор документа, который нужно снять с маршрута согласования.
- ``RouteId`` — идентификатор маршрута согласования, с которого нужно снять документ.
- ``Comment`` — текстовый комментарий. Длина не должна превышать 500 символов.
- ``Labels`` — список :doc:`меток <Labels>`.


.. _EditingPatch:

EditingPatch
------------

Структура ``EditingPatch`` представляет собой операцию по редактированию контента документа.

.. code-block:: protobuf

    message EditingPatch {
        required string ParentEntityId = 1;
        required UnsignedContent Content = 2;
        repeated string Labels = 3;
    }

..

- ``ParentEntityId`` — идентификатор документа, контент которого нужно отредактировать. Принимает значение одной из :doc:`сущностей <Entity message>` родительского сообщения (поле ``EntityId``).
- ``Content`` — новое содержимое документа, представленное структурой :doc:`UnsignedContent`.
- ``Labels`` — список :doc:`меток <Labels>`.


----

.. rubric:: См. также

*Структура используется:*
	- в теле запроса метода :doc:`../http/PostMessagePatch`.