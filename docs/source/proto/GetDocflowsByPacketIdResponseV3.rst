GetDocflowsByPacketIdResponseV3
===============================

Структура ``GetDocflowsByPacketIdResponseV3`` представляет собой список документов, полученных методом :doc:`../http/GetDocflowsByPacketId_V3`.

.. code-block:: protobuf

   message GetDocflowsByPacketIdResponseV3
   {
       repeated FetchedDocumentV3 Documents = 1;
       optional bytes NextPageIndexKey = 2;
   }

- ``Documents`` — список документов в пакете, представленный структурой :doc:`FetchedDocumentV3`.
- ``NextPageIndexKey`` — ключ, использующийся для постраничного получения документов. Возвращается в том случае, когда количество документов, соответствующих запросу, превышает допустимый размер страницы.

----

Смотри также
^^^^^^^^^^^^

Структура используется:
	- в теле ответа метода :doc:`../http/GetDocflowsByPacketId_V3`.