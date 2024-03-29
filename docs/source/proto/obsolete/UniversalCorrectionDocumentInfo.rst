UniversalCorrectionDocumentInfo
===============================

.. warning::
	Структура относится к устаревшей версии Docflow API. Используйте последнюю версию :doc:`../../Docflow API` — V3.

Структура ``UniversalCorrectionDocumentInfo`` представляет собой метаданные документов, имеющих :doc:`тип <DocumentType>` ``UniversalCorrectionDocument`` и ``UniversalCorrectionDocumentRevision``.

.. code-block:: protobuf

    message UniversalCorrectionDocumentInfo
    {
        optional string TotalInc = 1;
        optional string TotalDec = 2;
        optional string VatInc = 3;
        optional string VatDec = 4;
        optional int32 CurrencyCode = 5;
        optional string Grounds = 6;
        required FunctionType Function = 7;
        optional DocumentDateAndNumber OriginalDocumentDateAndNumber = 8;
        optional DocumentDateAndNumber OriginalDocumentRevisionDateAndNumber = 9;
        optional DocumentDateAndNumber OriginalDocumentCorrectionDateAndNumber = 10;
    }

- ``TotalInc`` — сумма с учетом налога, всего к увеличению.
- ``TotalDec`` — сумма с учетом налога, всего к уменьшению.
- ``VatInc`` — сумма налога, всего к увеличению.
- ``VatDec`` — сумма налога, всего к уменьшению.
- ``CurrencyCode`` — код валюты.
- ``Grounds`` — описание оснований для данного документа.
- ``Function`` — функция документа, описывается структурой :doc:`FunctionType <UniversalTransferDocumentSellerTitleInfo>`.
- ``OriginalDocumentDateAndNumber`` — дата и номер исходного УПД, представленные структурой :doc:`../DocumentDateAndNumber`. Заполняется только если корректировка была сформирована на УПД. 
- ``OriginalDocumentRevisionDateAndNumber`` — дата и номер исходного исправления УПД, представленные структурой :doc:`../DocumentDateAndNumber`. Заполняется только если корректировка была сформирована на исправление УПД.
- ``OriginalDocumentCorrectionDateAndNumber`` — дата и номер исходной УКД, представленные структурой :doc:`../DocumentDateAndNumber`. Заполняется только если корректировка была сформирована на УКД.

----

.. rubric:: Смотри также

*Структура используется:*
	- в структуре :doc:`DocumentInfo`.

*Руководства:*
	- :doc:`../../Docflow API`