DocumentLinks
=============

.. warning:: Эта версия контракта — экспериментальная и может измениться.

.. code-block:: protobuf

    message DocumentLinks
    {
        repeated DocumentId InitialIds = 1;
        repeated DocumentId SubordinateIds = 2;
    }

Структура содержит информацию о связанных документах.

- :doc:`InitialIds <DocumentId>` - список идентификаторов документов, на которые ссылается данный
- :doc:`SubordinateIds <DocumentId>` - список идентификаторов документов, которые ссылаются на данный
