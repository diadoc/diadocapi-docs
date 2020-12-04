FetchedDocumentV3
=================

.. code-block:: protobuf

   message FetchedDocumentV3
   {
       required DocumentWithDocflowV3 Document = 1;
       required bytes IndexKey = 2;
   }

Структура представляет один документ из списка, возвращаемого методом :doc:`../http/GetDocflowsByPacketId_V3`.

-  :doc:`Document <DocumentWithDocflowV3>` - информация о документе: метаданные и состояние документооборота.
-  *IndexKey* - ключ, используемый для постраничной выгрузки достаточно большого количества документов из одного пакета. При передаче в метод :doc:`../http/GetDocflowsByPacketId_V3`, позволяет пропустить те документы, которые были выгружены ранее, до данного документа включительно.
