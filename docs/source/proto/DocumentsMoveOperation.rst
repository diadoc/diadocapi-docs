DocumentsMoveOperation
======================

Структура ``DocumentsMoveOperation`` хранит информацию для перемещения документов между подразделениями организации.

.. code-block:: protobuf

    message DocumentsMoveOperation
    {
        required string BoxId = 1;
        optional string ToDepartmentId = 2;
        repeated DocumentId DocumentIds = 3;
    }

- ``BoxId`` — идентификатор ящика, в котором находятся документы.
- ``ToDepartmentId`` — идентификатор подразделения, в которое нужно переместить документы.
- ``DocumentIds`` — список идентификаторов документов, которые нужно переместить, представленных структурой :doc:`DocumentId`.


----

.. rubric:: См. также

*Структура используется:*
	- в теле запроса метода :doc:`../http/MoveDocuments`
