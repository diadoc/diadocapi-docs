PriceListDocumentInfo
=====================

.. code-block:: protobuf

   message PriceListDocumentInfo
   {
       optional string PriceListEffectiveDate = 1;
       optional DocumentDateAndNumber ContractDocumentDateAndNumber = 2;
   }

Структура представляет метаданные документов, имеющих :doc:`тип <DocumentType>` PriceList.

-  *PriceListEffectiveDate* - дата вступления в силу ценового листа (в формате ДД.ММ.ГГГГ).
-  :doc:`ContractDocumentDateAndNumber <DocumentDateAndNumber>` - дата составления и номер договора, к которому относится ценовой лист.
