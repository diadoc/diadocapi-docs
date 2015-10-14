SupplementaryAgreementDocumentInfo
==================================

.. code-block:: protobuf

    message SupplementaryAgreementDocumentInfo
	{
		optional string Total = 1;
		optional string ContractType = 2;
		optional string ContractNumber = 3;
		optional string ContractDate = 4;
	}

Структура представляет метаданные документов, имеющих :doc:`тип <DocumentType>` *SupplementaryAgreement*.

-  *Total* - цена дополнительного соглашения к договору.

-  *ContractType* - тип договора.

-  *ContractNumber* - номер договора.

-  *ContractDate* - дата договора.
