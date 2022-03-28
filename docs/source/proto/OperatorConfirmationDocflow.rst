OperatorConfirmationDocflow
===========================

.. code-block:: protobuf

    message OperatorConfirmationDocflow
    {
        optional SignedAttachmentV3 ConfirmationAttachment = 1;
        optional Timestamp ConfirmedAt = 2;
    }

Структура содержит информацию о подтверждении оператора ЭДО.

- ``ConfirmationAttachment`` — данные о файле подтверждения оператора и подписи под ним, представленные структурой :doc:`SignedAttachmentV3`.
- ``ConfirmedAt`` — дата подтверждения оператора, представленная структурой :doc:`Timestamp`.

----

.. rubric:: Использование

Структура ``OperatorConfirmationDocflow`` используется в структуре :doc:`ConfirmationDocflow`.