GetDocflowsByPacketIdResponseV3
===============================

.. code-block:: protobuf

   message GetDocflowsByPacketIdResponseV3
   {
       repeated FetchedDocumentV3 Documents = 1;
       optional bytes NextPageIndexKey = 2;
   }

Представляет результат работы метода :doc:`../http/GetDocflowsByPacketId_V3`.

-  :doc:`Documents <FetchedDocumentV3>` - список документов, содержащихся в пакете.
-  *NextPageIndexKey* - ключ, использующийся для постраничной выгрузки. Заполняется в том случае, когда количество документов, соответствующих запросу, превышает допустимый размер страницы.
