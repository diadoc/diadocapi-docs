TemplateTransformationToPost
============================

Содержит информацию для создания документов на основе шаблонов.

.. code-block:: protobuf

    message TemplateTransformationToPost {
        required string BoxId = 1;
        required string TemplateId = 2;
        repeated DocumentTransformation DocumentTransformations = 3;
    }

- *BoxId* - идентификатор ящика отправителя.

- *TemplateId* - идентификатор шаблона с документами для преобразования.

- *DocumentTransformations* - список сообщений с идентификаторами обрабатываемых документов. Каждое сообщение задается структурой :doc:`DocumentTransformation`.
