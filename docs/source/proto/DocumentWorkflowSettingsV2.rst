DocumentWorkflowSettingsV2
==========================

Структура ``DocumentWorkflowSettingsV2`` хранит информацию о свойствах :doc:`вида документооборота <../proto/DocumentWorkflow>`.

.. code-block:: protobuf

    message DocumentWorkflowSettings {
        required int32 Id = 1;
        repeated ParticipantSettingV2 Participants = 2;
        required OperatorConfirmationReceiptBehavior OperatorConfirmationReceiptBehavior = 3;
        required ReceiptOperatorConfirmationReceiptBehavior ReceiptOperatorConfirmationReceiptBehavior = 4;
        required OperatorConfirmationBehavior ReceiptOperatorConfirmationBehavior = 5;
        required AmendmentRequestResponseBehavior AmendmentRequestResponseBehavior = 6;
        required RoamingConfirmationBehavior ReceiptRoamingConfirmationBehavior = 7;
        required InvitationBehavior InvitationBehavior = 8;
    }

    message ParticipantSettingV2 {
        required ParticipantType Participant = 1;
        required ParticipantAction ParticipantAction = 2;
        required TitleReceiptBehavior TitleReceiptBehavior = 3;
    }

    enum OperatorConfirmationReceiptBehavior {
        Unknown = 0;
        Never = 1;
        Always = 2;
    }

    enum ReceiptOperatorConfirmationReceiptBehavior {
        Unknown = 0;
        Never = 1;
        Always = 2;
    }

    enum OperatorConfirmationBehavior {
        Unknown = 0;
        Never = 1;
        Initiator = 2;
        InitiatorCounterpart = 3;
    }

    enum AmendmentRequestResponseBehavior {
        Unknown = 0;
        None = 1;
        Receipt = 2;
        OperatorConfirmation = 3;
        OperatorConfirmationOrReceipt = 4;
    }

    enum RoamingConfirmationBehavior {
        Unknown = 0;
        Never = 1;
        Always = 2;
    }

    enum InvitationBehavior {
        Unknown = 0;
        Never = 1;
        DefineByUser = 2;
        Always = 3;
    }

    enum ParticipantType {
        Unknown = 0;
        Sender = 1;
        Proxy = 2;
        Recipient = 3;
    }

    enum ParticipantAction {
        Unknown = 0;
        Title = 1;
        Signature = 2;
        OptionalSignature = 3;
    }

    enum TitleReceiptBehavior {
        Unknown = 0;
        Never = 1;
        DefineByUser = 2;
        Always = 3;
    }

В описании используются следующие сокращения:
 - **ИоП** — извещение о получении.
 - **УоУ** — уведомление об уточнении.

- ``Id`` — уникальный числовой идентификатор документооборота.
- ``Participants`` — список участников документооборота и их свойства. Представлены структурой ``ParticipantSettingV2`` с полями:

	- ``Participant`` — идентификатор участника документооборота, принимает значения из перечисления ``ParticipantType``:

		- ``Sender`` — отправитель;
		- ``Proxy`` — промежуточный получатель;
		- ``Recipient`` — получатель;

	- ``ParticipantAction`` — свойство «Действие участника», принимает значения из перечисления ``ParticipantAction``:
	
		- ``Title`` — титул;
		- ``Signature`` — подпись;
		- ``OptionalSignature`` — подпись по запросу;

	- ``TitleReceiptBehavior`` — свойство «ИоП на титул участника», принимает значения из перечисления ``TitleReceiptBehavior``:

		- ``Never`` — не требуется;
		- ``DefineByUser`` — по запросу;
		- ``Always`` — требуется.

- ``OperatorConfirmationReceiptBehavior`` — свойство «ИоП на подтверждение оператора», принимает значения из перечисления ``OperatorConfirmationReceiptBehavior``:

	- ``Never`` — не требуется;
	- ``Always`` — требуется.

- ``ReceiptOperatorConfirmationReceiptBehavior`` — свойство «ИоП на подтверждение оператора на ИоП», принимает значения из перечисления ``ReceiptOperatorConfirmationReceiptBehavior``:

	- ``Never`` — не требуется;
	- ``Always`` — требуется.

- ``ReceiptOperatorConfirmationBehavior`` — свойство «Подтверждение оператора на ИоП», принимает значения из перечисления ``OperatorConfirmationBehavior``:

	- ``Never`` — не требуется;
	- ``Initiator`` — подтверждение оператора должно быть отправлено отправителю;
	- ``InitiatorCounterpart`` — подтверждение оператора должно быть отправлено отправителю и получателю.

- ``AmendmentRequestResponseBehavior`` — свойство «Ответное действие на УоУ», принимает значения из перечисления ``AmendmentRequestResponseBehavior``:

	- ``None`` — нет;
	- ``Receipt`` — ИоП;
	- ``OperatorConfirmation`` — подтверждение оператора;
	- ``OperatorConfirmationOrReceipt`` — подтверждение оператора или ИоП.

- ``ReceiptRoamingConfirmationBehavior`` — свойство «Подтверждение оператора из роуминга на ИоП», принимает значения из перечисления ``RoamingConfirmationBehavior``:

	- ``Never`` — не требуется;
	- ``Always`` — требуется.

- ``InvitationBehavior`` — свойство «Используется как приглашение», принимает значения из перечисления ``InvitationBehavior``:

	- ``Never`` — не требуется;
	- ``DefineByUser`` — по запросу;
	- ``Always`` — требуется.

----

.. rubric:: См. также

*Структура используется:*
	- в теле ответа метода :doc:`../http/GetWorkflowsSettings`
	
*Руководства:*
	- :doc:`../docflows/Workflows`