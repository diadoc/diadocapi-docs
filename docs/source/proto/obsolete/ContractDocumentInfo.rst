ContractDocumentInfo
====================

.. warning::
	Структура относится к устаревшей версии Docflow API. Используйте последнюю версию :doc:`../../Docflow API` — V3.

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
	- в структуре :doc:`DocumentInfo`.

*Руководства:*
	- :doc:`../../Docflow API`