FetchedDocument
===============

.. code-block:: protobuf

   message FetchedDocument
   {
       required DocumentWithDocflow Document = 1;
       required bytes IndexKey = 2;
   }

Структура представляет один документ из списка, возвращаемого методом :doc:`../http/GetDocflowsByPacketId`.

-  :doc:`Document <DocumentWithDocflow>` - информация о документе: метаданные и состояние документооборота.
-  *IndexKey* - ключ, используемый для постраничной выгрузки достаточно большого количества документов из одного пакета. При передаче в метод :doc:`../http/GetDocflowsByPacketId`, позволяет пропустить те документы, которые были выгружены ранее, до данного документа включительно.
