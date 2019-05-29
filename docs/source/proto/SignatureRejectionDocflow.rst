SignatureRejectionDocflow
=========================

.. warning:: Эта версия контракта — экспериментальная и может измениться.

.. code-block:: protobuf

    message SignatureRejectionDocflow
    {
        required SignedAttachmentV3 SignatureRejection = 1;
        required bool IsFormal = 2;
        optional Timestamp DeliveredAt = 3;
        optional string PlainText = 4;
    }

Структура содержит информацию об отказе в подписи.


- :doc:`SignatureRejection <SignedAttachmentV3>` - данные о файле отказа в подписи и подписи под ним
- *IsFormal* - является ли отказ в подписи формализованным
- :doc:`DeliveredAt <Timestamp>` - метка времени доставки отказа в подписи в ящик контрагента
- *PlainText* - текст сообщения об отказе в подписи
