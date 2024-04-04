SupplementaryAgreementDocumentInfo
==================================

.. warning::
	Структура относится к устаревшей версии Docflow API. Используйте последнюю версию :doc:`../../Docflow API` — V3.

Структура ``SupplementaryAgreementDocumentInfo`` представляет собой метаданные документов, имеющих :doc:`тип <DocumentType>` ``SupplementaryAgreement``.

.. code-block:: protobuf

    message SupplementaryAgreementDocumentInfo
    {
        optional string ContractType = 1;
        required DocumentDateAndNumber ContractDocumentDateAndNumber = 2;
        required DocumentDateAndNumber DocumentDateAndNumber = 3;
        optional string Total = 4;
    }

- ``ContractType`` — тип договора.
- ``ContractDocumentDateAndNumber`` — номер и дата договора, представленные структурой :doc:`../DocumentDateAndNumber`.
- ``DocumentDateAndNumber`` — номер и дата документа, представленные структурой :doc:`../DocumentDateAndNumber`.
- ``Total`` — цена дополнительного соглашения к договору.

----

.. rubric:: См. также

*Структура используется:*
	- в структуре :doc:`DocumentInfo`.

*Руководства:*
	- :doc:`../../Docflow API`