DocumentDateAndNumber
=====================

.. warning::
	Структура устарела.

Структура ``DocumentDateAndNumber`` представляет собой дату и номер документа.

У формализованных документов эти поля хранятся в самом файле, у полуформализованных документов они указываются пользователем при отправке.

.. code-block:: protobuf

    message DocumentDateAndNumber
    {
        optional string DocumentDate = 1;
        optional string DocumentNumber = 2;
    }

- ``DocumentDate`` — дата документа.
- ``DocumentNumber`` — номер документа.


----

.. rubric:: См. также

*Структура используется:*
	- в устаревшей структуре :doc:`DocumentInfo`
	- в устаревшей структуре :doc:`EncryptedDocumentMetadata`
	- в устаревшей структуре :doc:`EncryptedInvoiceMetadata <EncryptedInvoiceAttachment>`
	- в устаревшей структуре :doc:`EncryptedInvoiceCorrectionMetadata <EncryptedInvoiceAttachment>`
	- в устаревшей структуре :doc:`InvoiceCorrectionDocumentInfo`
	- в устаревшей структуре :doc:`InvoiceDocumentInfo`
	- в устаревшей структуре :doc:`PriceListDocumentInfo`
	- в устаревшей структуре :doc:`SupplementaryAgreementDocumentInfo`
	- в устаревшей структуре :doc:`UniversalCorrectionDocumentInfo`
	- в устаревшей структуре :doc:`UniversalTransferDocumentInfo`