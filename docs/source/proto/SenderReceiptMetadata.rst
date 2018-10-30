SenderReceiptMetadata
========================

Содержит информацию об извещении о получении титула получателя.

.. code-block:: protobuf

    message SenderReceiptMetadata {
        required GeneralReceiptStatus ReceiptStatus = 1;
    }


- :doc:`ReceiptStatus <GeneralReceiptStatus>` - статус извещения о получении титула получателя.