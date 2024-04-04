InvoiceCorrectionDocumentInfo
=============================

.. warning::
	Структура относится к устаревшей версии Docflow API. Используйте последнюю версию :doc:`../../Docflow API` — V3.

Структура ``InvoiceCorrectionDocumentInfo`` представляет собой метаданные документов, имеющих :doc:`тип <DocumentType>` ``InvoiceCorrection`` или ``InvoiceCorrectionRevision``.

.. code-block:: protobuf

    message InvoiceCorrectionDocumentInfo
    {
        optional string TotalInc = 1;
        optional string TotalDec = 2;
        optional string VatInc = 3;
        optional string VatDec = 4;
        optional int32 CurrencyCode = 5;
        optional DocumentDateAndNumber OriginalInvoiceDateAndNumber = 6;
        optional DocumentDateAndNumber OriginalInvoiceRevisionDateAndNumber = 7;
        optional DocumentDateAndNumber OriginalInvoiceCorrectionDateAndNumber = 8;
    }

- ``TotalInc`` — сумма с учетом налога, всего к увеличению.
- ``TotalDec`` — сумма с учетом налога, всего к уменьшению.
- ``VatInc`` — сумма налога, всего к увеличению.
- ``VatDec`` — сумма налога, всего к уменьшению.
- ``CurrencyCode`` — код валюты.
- ``OriginalInvoiceDateAndNumber`` — дата и номер исходного счета-фактуры, представленные структурой :doc:`../DocumentDateAndNumber`. Заполняется только если корректировка была сформирована на счет-фактуру.
- ``OriginalInvoiceRevisionDateAndNumber`` — дата и номер исходного исправления счета-фактуры, представленные структурой :doc:`../DocumentDateAndNumber`. Заполняется только если корректировка была сформирована на исправление счета-фактуры.
- ``OriginalInvoiceCorrectionDateAndNumber`` — дата и номер исходной корректировки счета-фактуры, представленные структурой :doc:`../DocumentDateAndNumber`. Заполняется только если корректировка была сформирована на корректировку счета-фактуры.

----

.. rubric:: См. также

*Структура используется:*
	- в структуре :doc:`DocumentInfo`