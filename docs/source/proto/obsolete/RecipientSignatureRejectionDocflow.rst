RecipientSignatureRejectionDocflow
==================================

.. warning::
	Структура относится к устаревшей версии Docflow API. Используйте последнюю версию :doc:`../../Docflow API` — V3.

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
	- в структуре :doc:`BilateralDocflow`
	- в структуре :doc:`InboundUniversalTransferDocumentDocflow`
	- в структуре :doc:`OutboundUniversalTransferDocumentDocflow`
	- в структуре :doc:`RevocationDocflow`
	- в структуре :doc:`XmlBilateralDocflow`