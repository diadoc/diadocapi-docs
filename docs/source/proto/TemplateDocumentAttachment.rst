TemplateDocumentAttachment
==================

    :synopsis: Представляет в отправляемом сообщении :doc:`TemplateToPost` документ любого типа.

.. code-block:: protobuf

    message TemplateDocumentAttachment {
        required UnsignedContent UnsignedContent = 1;
        optional string Comment = 2;
        required string TypeNamedId = 3;
        optional string Function = 4;
        optional string Version = 5;
        repeated MetadataItem Metadata = 6;
        optional int32 WorkflowId = 7;
        optional string CustomDocumentId = 8;
    }

    :param UnsignedContent: содержимое файла в виде структуры :doc:`UnsignedContent`.

    :param Comment: необязательный текстовый комментарий к документу.

    :param TypeNamedId: строковой идентификатор типа документа. Доступные типы можно получить методом :doc:`../http/GetDocumentTypes`.

    :param Function: идентификатор функции документа. Обязательно при отправке зашифрованных документов.

    :param Version: идентификатор версии документа. Обязательно при отправке зашифрованных документов.

    :param Metadata: список пар вида "ключ-значение", содержащих метаданные документа. Каждая пара задается структурой :doc:`MetadataItem`. Список доступных метаданных для типа можно получить через метод :doc:`../http/GetDocumentTypes`.

    :param WorkflowId: идентификатор вида документооборота. Список допустимых видов документооборота для типа можно получить через метод :doc:`../http/GetDocumentTypes`. Описание видов документооборота доступно на странице :doc:`DocumentWorkflow`.

    :param CustomDocumentId: необязательный идентификатор документа во внешней системе, уникальный в рамках структуры :doc:`TemplateToPost`; используется для выстраивания связей между документами внутри отправляемого сообщения. В дальнейшем его можно получить через *Document.CustomDocumentId*.