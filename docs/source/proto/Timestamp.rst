Timestamp
=========

Структура ``Timestamp`` представляет собой момент времени без привязки к часовому поясу (UTC-время).

.. code-block:: protobuf

    message Timestamp
    {
        required sfixed64 Ticks = 1;
    }

- ``Ticks`` - целое число тиков (100-наносекундных интервалов), прошедших с момента времени 00:00:00 01.01.0001.


Примеры использования
---------------------

**Пример преобразования Timestamp в DateTime (C#):**

.. code-block:: csharp

	var dt = new DateTime(timestamp.Ticks, DateTimeKind.Utc);


----

.. rubric:: См. также

*Структура используется:*
	- в структуре :doc:`AmendmentRequestDocflow`
	- в структуре :doc:`CertificateVerificationResult`
	- в структуре :doc:`ConfirmationDocflow`
	- в структуре :doc:`Department`
	- в структуре :doc:`DocflowEventV3`
	- в структуре :doc:`Employee`
	- в структуре :doc:`Entity`
	- в структуре :doc:`ForwardDocumentEvent`
	- в структуре :doc:`ForwardedDocument`
	- в структуре :doc:`LastEvent <DocumentWithDocflowV3>`
	- в структуре :doc:`OperatorConfirmationDocflow`
	- в структуре :doc:`PacketInfo`
	- в структуре :doc:`ParticipantResponseDocflow`
	- в структуре :doc:`PowerOfAttorney`
	- в структуре :doc:`PowerOfAttorneyStatus <PowerOfAttorneyRegisterResult>`
	- в структуре :doc:`ReceiptDocflowV3`
	- в структуре :doc:`RevocationRequestDocflow <RevocationDocflowV3>`
	- в структуре :doc:`SenderTitleDocflow`
	- в структуре :doc:`SignatureInfo`
	- в структуре :doc:`SignatureRejectionDocflow`
	- в структуре :doc:`SignatureV3`
	- в структуре :doc:`SignatureVerificationResult`
	- в структуре :doc:`TimeBasedFilter`
	- в структуре ``ForwardDocumentResponse``, возвращаемой методом :doc:`../http/ForwardDocument`
	- в структуре ``ForwardedDocumentEvent``, возвращаемой методом :doc:`../http/GetForwardedDocumentEvents`
	- в устаревшей структуре :doc:`obsolete/BuyerTitleDocflow`
	- в устаревшей структуре :doc:`obsolete/Docflow`
	- в устаревшей структуре :doc:`obsolete/DocflowEvent`
	- в устаревшей структуре :doc:`obsolete/DocumentWithDocflow`
	- в устаревшей структуре :doc:`obsolete/InboundInvoiceDocflow`
	- в устаревшей структуре :doc:`obsolete/InboundUniversalTransferDocumentDocflow`
	- в устаревшей структуре :doc:`obsolete/OutboundInvoiceDocflow`
	- в устаревшей структуре :doc:`obsolete/OutboundUniversalTransferDocumentDocflow`
	- в устаревшей структуре :doc:`obsolete/RecipientSignatureDocflow`
	- в устаревшей структуре :doc:`obsolete/RecipientSignatureRejectionDocflow`