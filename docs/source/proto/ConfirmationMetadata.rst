ConfirmationMetadata
====================

Структура ``ConfirmationMetadata`` представляет собой сформированное оператором ЭДО подтверждение даты отправки/получения документа или извещения о получении.

.. code-block:: protobuf

    message ConfirmationMetadata {
        required GeneralReceiptStatus ReceiptStatus = 1;
        required sfixed64 DateTimeTicks = 2;
    }

- ``ReceiptStatus`` — статус извещения о получении под подтверждением даты, представленный структурой :doc:`GeneralReceiptStatus`.
- ``DateTimeTicks`` — время создания оператором подтверждения даты отправки/получения в московском часовом поясе (GMT+4). Представляет собой целое число тиков, прошедших с момента времени 00:00:00 01.01.0001. Для документов, которые на поддерживают подтверждение, будет равно нулю.


----

.. rubric:: См. также

*Структура используется:*
	- в структуре :doc:`Document`
	- в структуре :doc:`RecipientReceiptMetadata`