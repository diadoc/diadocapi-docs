ContractDocumentInfo
====================

.. code-block:: protobuf

    message ContractDocumentInfo
    {
        optional string ContractPrice = 1;
        optional string ContractType = 2;
    }

Структура представляет метаданные документов, имеющих :doc:`тип <DocumentType>` *Contract*.

-  *ContractPrice* - цена, указанная в договоре.
-  *ContractType* - тип договора.
