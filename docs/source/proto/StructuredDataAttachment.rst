StructuredDataAttachment
========================

Структура ``StructuredDataAttachment`` представляет собой файл со структурированными данными в отправляемом сообщении :doc:`MessageToPost`. С помощью этой структуры можно приложить к документу дополнительные данные в виде отдельного файла: например, печатную форму, QR-код или файл в определенном формате.

.. code-block:: protobuf

    message StructuredDataAttachment {
        required bytes Content = 1;
        required string FileName = 2;
        required string DocumentId = 3;
    }

- ``Content`` — содержимое файла размером до 10 Мбайт.
- ``FileName`` — имя файла.
- ``DocumentId`` — идентификатор, уникальный в рамках структуры ``MessageToPost``, с помощью которого файл связывается с соответствующим документом внутри отправляемого сообщения.


----

.. rubric:: См. также

*Структура используется:*
	- в структуре :doc:`MessageToPost`