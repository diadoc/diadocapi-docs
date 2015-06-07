GetDocflowsByPacketIdResponse
=============================

.. code-block:: protobuf

   message GetDocflowsByPacketIdResponse
   {
       repeated FetchedDocument Documents = 1;
       optional bytes NextPageIndexKey = 2;
   }

Представляет результат работы метода :doc:`../http/GetDocflowsByPacketId`.

-  :doc:`Documents <FetchedDocument>` - список документов, содержащихся в пакете.
-  *NextPageIndexKey* - ключ, использующийся для постраничной выгрузки. Заполняется в том случае, когда количество документов, соответствующих запросу, превышает допустимый размер страницы.
