InvoiceDocumentInfo
===================

.. warning::
	Структура относится к устаревшей версии Docflow API. Используйте последнюю версию :doc:`../../Docflow API` — V3.

Структура ``InvoiceDocumentInfo`` представляет собой метаданные документов, имеющих :doc:`тип <DocumentType>` ``Invoice`` или ``InvoiceRevision``.

.. code-block:: protobuf

    message InvoiceDocumentInfo
    {
        optional string Total = 1;
        optional string Vat = 2;
        optional int32 CurrencyCode = 3;
        optional DocumentDateAndNumber OriginalInvoiceDateAndNumber = 4;
    }

- ``Total`` — сумма с учетом НДС, всего по документу.
- ``Vat`` — сумма НДС, всего по документу.
- ``CurrencyCode`` — код валюты.
- ``OriginalInvoiceDateAndNumber`` — дата и номер исходного счета-фактуры, представленные структурой :doc:`../DocumentDateAndNumber`. Заполняется только для документов с типом ``InvoiceRevision``.

----

.. rubric:: См. также

*Структура используется:*
	- в структуре :doc:`DocumentInfo`