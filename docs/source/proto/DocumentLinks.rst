DocumentLinks
=============

Структура ``DocumentLinks`` содержит информацию о связанных документах.

.. code-block:: protobuf

    message DocumentLinks
    {
        repeated DocumentId InitialIds = 1;
        repeated DocumentId SubordinateIds = 2;
    }

- ``InitialIds`` - список идентификаторов документов, на которые ссылается данный документ. Каждый элемент списка представлен структурой :doc:`DocumentId`.
- ``SubordinateIds`` - список идентификаторов документов, которые ссылаются на данный документ. Каждый элемент списка представлен структурой :doc:`DocumentId`.


----

.. rubric:: См. также

*Структура используется:*
	- в структуре :doc:`DocumentInfoV3`