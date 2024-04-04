UniversalTransferDocumentInfo
=============================

.. warning::
	Структура относится к устаревшей версии Docflow API. Используйте последнюю версию :doc:`../../Docflow API` — V3.

Структура ``UniversalTransferDocumentInfo`` представляет собой метаданные документов, имеющих :doc:`тип <DocumentType>` ``UniversalTransferDocument`` и ``UniversalTransferDocumentRevision``.

.. code-block:: protobuf

    message UniversalTransferDocumentInfo
    {
        optional string Total = 1;
        optional string Vat = 2;
        optional int32 CurrencyCode = 3;
        optional string Grounds = 4;
        required FunctionType Function = 5;
        optional DocumentDateAndNumber OriginalDocumentDateAndNumber = 6;
    }

- ``Total`` — сумма с учетом НДС, всего по документу.
- ``Vat`` — сумма НДС, всего по документу.
- ``CurrencyCode`` — код валюты.
- ``Grounds`` — описание оснований для данного документа.
- ``Function`` — функция документа, представленная структурой :doc:`FunctionType <UniversalTransferDocumentSellerTitleInfo>`.
- ``OriginalDocumentDateAndNumber`` — дата и номер исходного УПД, представленные структурой :doc:`../DocumentDateAndNumber`. Заполняется только для ``UniversalTransferDocumentRevision``.

----

.. rubric:: См. также

*Структура используется:*
	- в структуре :doc:`DocumentInfo`