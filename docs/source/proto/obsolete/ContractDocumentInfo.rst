ContractDocumentInfo
====================

.. warning::
	Структура используется внутри устаревшей структуры :doc:`DocumentInfo`.

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
	- в структуре :doc:`DocumentInfo`