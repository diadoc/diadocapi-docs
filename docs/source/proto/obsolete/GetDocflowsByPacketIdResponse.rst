GetDocflowsByPacketIdResponse
=============================

.. warning::
	Структура устарела. Вместо нее используется структура :doc:`../GetDocflowsByPacketIdResponseV3`.

Структура ``GetDocflowsByPacketIdResponse`` представляет собой список документов, полученных методом :doc:`../../http/obsolete/GetDocflowsByPacketId_v2`.

.. code-block:: protobuf

   message GetDocflowsByPacketIdResponse
   {
       repeated FetchedDocument Documents = 1;
       optional bytes NextPageIndexKey = 2;
   }

- ``Documents`` — список документов в пакете, представленный структурой :doc:`FetchedDocument`.
- ``NextPageIndexKey`` — ключ, использующийся для постраничного получения документов. Возвращается в том случае, когда количество документов, соответствующих запросу, превышает допустимый размер страницы.

----

.. rubric:: См. также

*Структура используется:*
	- в теле ответа метода :doc:`../../http/obsolete/GetDocflowsByPacketId_v2`