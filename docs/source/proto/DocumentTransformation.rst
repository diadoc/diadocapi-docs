DocumentTransformation
======================

Содержит информацию о документе для трансформации из шаблона.

.. code-block:: protobuf

    message DocumentTransformation {
        required string DocumentId = 1;
        optional string CustomDocumentId = 2;
    }

- *DocumentId* - идентификатор документа для преобразования из шаблона.

- *CustomDocumentId* - необязательный идентификатор документа во внешней системе; используется для выстраивания связей между документами внутри отправляемого сообщения. В дальнейшем его можно получить через *Document.CustomDocumentId*.
