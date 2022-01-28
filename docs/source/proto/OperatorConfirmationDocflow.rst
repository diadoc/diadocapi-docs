OperatorConfirmationDocflow
===========================

.. warning:: Эта версия контракта — экспериментальная и может измениться.

.. code-block:: protobuf

    message OperatorConfirmationDocflow
    {
        optional SignedAttachmentV3 ConfirmationAttachment = 1;
        optional Timestamp ConfirmedAt = 2;
    }

Структура содержит информацию о подтверждении оператора ЭДО. Содержится в структуре :doc:`ConfirmationDocflow`.

- :doc:`ConfirmationAttachment <SignedAttachmentV3>` — данные о файле подтверждения оператора и подписи под ним
- :doc:`ConfirmedAt <Timestamp>` — дата подтверждения оператора