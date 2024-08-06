ContractDocumentInfo
====================

.. warning::
	Структура устарела.

Структура ``ContractDocumentInfo`` представляет собой метаданные документов, имеющих :doc:`тип <DocumentType>` ``Contract``.

.. code-block:: protobuf

    message ContractDocumentInfo
    {
        optional string ContractPrice = 1;
        optional string ContractType = 2;
    }

- ``ContractPrice`` — цена, указанная в договоре.
- ``ContractType`` — тип договора.


----

.. rubric:: См. также

*Структура используется:*
	- в устаревшей структуре :doc:`DocumentInfo`