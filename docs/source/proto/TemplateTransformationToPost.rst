TemplateTransformationToPost
============================

    :synopsis: Содержит информацию для создания документов на основе шаблонов.

.. code-block:: protobuf

    message TemplateTransformationToPost {
        required string BoxId = 1;
        required string TemplateId = 2;
        repeated DocumentTransformation DocumentTransformations = 3;
    }

    :param BoxId: - идентификатор ящика отправителя.

    :param TemplateId: - идентификатор шаблона с документами для преобразования.

    :param DocumentTransformations: - список сообщений с идентификаторами обрабатываемых документов. Каждое сообщение задается структурой :doc:`DocumentTransformation`.