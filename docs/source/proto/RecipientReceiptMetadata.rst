RecipientReceiptMetadata
========================

Содержит информацию об извещении о получении документа контрагентом.

.. code-block:: protobuf

    message RecipientReceiptMetadata {
        required GeneralReceiptStatus ReceiptStatus = 1;
        required ConfirmationMetadata ConfirmationMetadata = 2;
    }


- :doc:`ReceiptStatus <GeneralReceiptStatus>` - статус извещения о получении документа.

- :doc:`ConfirmationMetadata <ConfirmationMetadata>` - информация о подтверждении оператором даты отправки ИОПа. Свойство актуально только для входящего документа, поддерживающего подтверждение оператора, например, счета-фактуры или УПД с функциями СЧФ/СЧФДОП.