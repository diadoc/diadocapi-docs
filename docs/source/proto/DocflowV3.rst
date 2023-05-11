DocflowV3
=========

Структура ``DocflowV3`` хранит информацию о состоянии документооборота одного документа.

.. code-block:: protobuf

    message DocflowV3
    {
        required SenderTitleDocflow SenderTitle = 1;
        optional ConfirmationDocflow Confirmation = 2;
        optional ParticipantResponseDocflow ProxyResponse = 11;
        optional ReceiptDocflowV3 RecipientReceipt = 4;
        optional ParticipantResponseDocflow RecipientResponse = 5;
        optional AmendmentRequestDocflow AmendmentRequest = 6;
        optional RevocationDocflowV3 Revocation = 7;
        optional ReceiptDocflowV3 SenderReceipt = 8;
        optional ResolutionDocflowV3 Resolution = 9;
        optional ResolutionEntitiesV3 ResolutionEntities = 10;
        repeated OuterDocflow OuterDocflows = 12;
        repeated OuterDocflowEntities OuterDocflowEntities = 13;
        required DocflowStatusV3 DocflowStatus = 14;
    }

- ``SenderTitle`` — информация о титуле отправителя. Представлена структурой :doc:`SenderTitleDocflow`.
- ``Confirmation`` — информация о подтверждении даты доставки титула отправителя. Представлена структурой :doc:`ConfirmationDocflow`. Подтверждение даты доставки формирует оператор.
- ``ProxyResponse`` — информация об ответе промежуточного получателя. Представлена структурой :doc:`ParticipantResponseDocflow`. Поле ``Confirmation`` для ответа промежуточного получателя не заполняется.
- ``RecipientReceipt`` — информация об извещении о получении документа или титула отправителя для двухтитульного документа. Представлена структурой :doc:`ReceiptDocflowV3`.
- ``RecipientResponse`` — информация об ответном действии получателя: подписании документа, отправке второго титула или отказе в подписи. Представлена структурой :doc:`ParticipantResponseDocflow`.
- ``AmendmentRequest`` — информация о документообороте по запросу уточнения. Представлена структурой :doc:`AmendmentRequestDocflow`.
- ``Revocation`` — информация об аннулировании. Представлена структурой :doc:`RevocationDocflowV3`.
- ``SenderReceipt`` — информация об извещении о получении титула получателя для двухтитульного документа. Представлена структурой :doc:`ReceiptDocflowV3`.
- ``Resolution`` — информация об актуальном статусе согласования документа или его аннулирования. Представлена структурой :doc:`ResolutionDocflowV3`.
- ``ResolutionEntities`` — информация о сущностях, относящихся к согласованию документа или его аннулированию. Представлена структурой :doc:`ResolutionEntitiesV3`.
- ``OuterDocflows`` — информация о внешнем документообороте по документу или аннулированию, например, о статусе обработки документа с маркированными товарами в ГИС МТ "Честный ЗНАК". Представлена структурой :doc:`OuterDocflow`.
- ``OuterDocflowEntities`` — список сущностей, относящихся к внешнему документообороту по документу или аннулированию, представленных структурой :doc:`OuterDocflowEntities`.
- ``DocflowStatus`` — информация о статусе документооборота. Представлена структурой :doc:`DocflowStatusV3`.

----

.. rubric:: Смотри также

*Структура используется:*
	- в структуре :doc:`DocumentWithDocflowV3`, возвращаемой методами

		- :doc:`../http/GetDocflows_V3`,
		- :doc:`../http/GetDocflowsByPacketId_V3`,
		- :doc:`../http/SearchDocflows_V3`.