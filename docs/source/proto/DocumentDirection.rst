DocumentDirection
=================

Перечисление ``DocumentDirection`` представляет собой направление движения документа по отношению к ящику, от имени которого запрошена информация о документе.

.. code-block:: protobuf

    enum DocumentDirection
    {
        UnknownDocumentDirection = 0;
        Inbound = 1;
        Outbound = 2;
        Internal = 3;
    }

- ``UnknownDocumentDirection`` — зарезервировано для обратной совместимости.
- ``Inbound`` — входящий документ.
- ``Outbound`` — исходящий документ.
- ``Internal`` — внутренний документ.


----

.. rubric:: См. также

*Перечисление используется:*
	- в структуре :doc:`Document`
	- в структуре :doc:`DocumentInfoV3`
	- в структуре :doc:`GetDocflowEventsRequest`
	- в устаревшей структуре :doc:`obsolete/DocumentInfo`