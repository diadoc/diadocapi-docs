DocflowEvent
============

.. warning::
	Структура устарела. Вместо нее используется структура :doc:`../DocflowEventV3`.

Структура ``DocflowEvent`` представляет одно событие, полученное методом :doc:`../../http/obsolete/GetDocflowEvents`.

.. code-block:: protobuf

   message DocflowEvent
   {
       optional string EventId = 1;
       optional Timestamp Timestamp = 2;
       optional DocumentId DocumentId = 3;
       optional bytes IndexKey = 4;
       optional DocumentWithDocflow Document = 5;
       optional string PreviousEventId = 6;
       optional DocumentWithDocflow PreviousDocumentState = 7;
   }

- ``EventId`` — идентификатор события.
- ``Timestamp`` — время возникновения события, представленное структурой :doc:`../Timestamp`.
- ``DocumentId`` — идентификатор документа, с которым произошло событие, представленный структурой :doc:`../DocumentId`.
- ``IndexKey`` — ключ события, используемый для постраничной выгрузки. Указывает, с какого события загружать очередную страницу.
- ``Document`` — состояние документа после возникновения данного события, представленное структурой :doc:`DocumentWithDocflow`.
- ``PreviousEventId`` — идентификатор предыдущего события по документу.
- ``PreviousDocumentState`` — состояние документа после возникновения предыдущего события, т.е. до возникновения данного события. Представлено структурой :doc:`DocumentWithDocflow`. 

Сравнивая содержимое полей ``Document`` и ``PreviousDocumentState``, можно составить картину изменений, которые произошли с документом.

----

.. rubric:: См. также

*Структура используется:*
	- в структуре :doc:`GetDocflowEventsResponse`