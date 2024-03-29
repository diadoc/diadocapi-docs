FetchedDocument
===============

.. warning::
	Структура относится к устаревшей версии Docflow API. Используйте последнюю версию :doc:`../../Docflow API` — V3.

Структура ``FetchedDocument`` представляет собой один документ из списка, возвращаемого методом :doc:`../../http/obsolete/GetDocflowsByPacketId`.

.. code-block:: protobuf

   message FetchedDocument
   {
       required DocumentWithDocflow Document = 1;
       required bytes IndexKey = 2;
   }

- ``DocumentWithDocflow`` — информация о документе — метаданные и состояние документооборота. Представлена структрурой :doc:`DocumentWithDocflow`.
- ``IndexKey`` — ключ, используемый для постраничной загрузки документов из одного пакета. При передаче в метод :doc:`../../http/obsolete/GetDocflowsByPacketId` позволяет пропустить те документы, которые были выгружены ранее, до данного документа включительно.

----

.. rubric:: Смотри также

*Структура используется:*
	- в структуре :doc:`GetDocflowsByPacketIdResponse`.

*Руководства:*
	- :doc:`../../Docflow API`