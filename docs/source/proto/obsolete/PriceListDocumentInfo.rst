PriceListDocumentInfo
=====================

.. warning::
	Структура устарела.

Структура ``PriceListDocumentInfo`` представляет собой метаданные документов, имеющих :doc:`тип <DocumentType>` ``PriceList``.

.. code-block:: protobuf

    message PriceListDocumentInfo
    {
        optional string PriceListEffectiveDate = 1;
        optional DocumentDateAndNumber ContractDocumentDateAndNumber = 2;
    }

- ``PriceListEffectiveDate`` — дата вступления в силу ценового листа в формате «ДД.ММ.ГГГГ».
- ``ContractDocumentDateAndNumber`` - дата составления и номер договора, к которому относится ценовой лист, представленные структурой :doc:`DocumentDateAndNumber`.


----

.. rubric:: См. также

*Структура используется:*
	- в устаревшей структуре :doc:`DocumentInfo`