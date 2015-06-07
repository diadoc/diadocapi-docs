StructuredDataAttachment
========================

.. code-block:: protobuf

    message StructuredDataAttachment {
        required bytes Content = 1;
        required string FileName = 2;
        required string DocumentId = 3;
    }
        

Структура данных StructuredDataAttachment представляет один файл со структурированными данными в отправляемом сообщении :doc:`MessageToPost`, описывающий тот или иной документ, который представлен в виде печатной формы:

-  Content - содержимое файла со структурированными данными.

-  FileName - имя файла со структурированными данными.

-  DocumentId - обязательный идентификатор уникальный в рамках структуры MessageToPost, который служит для связывания файла со структурированными данными с соответствующим документом в виде печатной формы внутри отправляемого сообщения.