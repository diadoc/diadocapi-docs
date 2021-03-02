SupplementaryAgreementDocumentInfo
==================================

.. code-block:: protobuf

    message SupplementaryAgreementDocumentInfo
	{
		optional string ContractType = 1;
		required DocumentDateAndNumber ContractDocumentDateAndNumber = 2;
		required DocumentDateAndNumber DocumentDateAndNumber = 3;
		optional string Total = 4;
	}

Структура представляет метаданные документов, имеющих :doc:`тип <DocumentType>` *SupplementaryAgreement*.

-  *ContractType* - тип договора.

-  *ContractDocumentDateAndNumber* - номер и дата договора.

-  *DocumentDateAndNumber* - номер и дата документа.

-  *Total* - цена дополнительного соглашения к договору.
