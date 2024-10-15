FetchedDocument
===============

.. warning::
	Структура устарела.

Структура ``FetchedDocument`` представляет собой один документ из списка, возвращаемого методом :doc:`../../http/obsolete/GetDocflowsByPacketId_v2`.

.. code-block:: protobuf

   message FetchedDocument
   {
       required DocumentWithDocflow Document = 1;
       required bytes IndexKey = 2;
   }

- ``DocumentWithDocflow`` — информация о документе — метаданные и состояние документооборота. Представлена структрурой :doc:`DocumentWithDocflow`.
- ``IndexKey`` — ключ, используемый для постраничной загрузки документов из одного пакета. При передаче в метод :doc:`../../http/obsolete/GetDocflowsByPacketId_v2` позволяет пропустить те документы, которые были выгружены ранее, до данного документа включительно.


----

.. rubric:: См. также

*Структура используется:*
	- в устаревшей структуре :doc:`GetDocflowsByPacketIdResponse`