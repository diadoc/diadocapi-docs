RecipientSignatureRejectionDocflow
==================================

.. warning::
	Структура устарела.

Структура ``RecipientSignatureRejectionDocflow`` представляет собой информацию об отказе контрагента в подписании документа. Отказ является подписанным файлом установленного формата.

.. code-block:: protobuf

   message RecipientSignatureRejectionDocflow
   {
       optional bool IsFinished = 1;
       optional SignedAttachment RecipientSignatureRejectionAttachment = 2;
       optional Timestamp DeliveryTimestamp = 3;
   }

- ``IsFinished`` — признак того, что документооборот по отказу завершен. Принимает значение ``true`` в случае если подпись под отказом проверена и он доставлен контрагенту.
- ``RecipientSignatureRejectionAttachment`` — информация о файле отказа, представленная структурой :doc:`../SignedAttachment`.
- ``DeliveryTimestamp`` — время доставки отказа, представленное структурой :doc:`../Timestamp`.


----

.. rubric:: См. также

*Структура используется:*
	- в устаревшей структуре :doc:`BilateralDocflow`
	- в устаревшей структуре :doc:`InboundUniversalTransferDocumentDocflow`
	- в устаревшей структуре :doc:`OutboundUniversalTransferDocumentDocflow`
	- в устаревшей структуре :doc:`RevocationDocflow`
	- в устаревшей структуре :doc:`XmlBilateralDocflow`