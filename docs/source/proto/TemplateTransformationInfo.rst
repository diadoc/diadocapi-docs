TemplateTransformationInfo
============================

Cодержит информацию о документе, созданном на основе шаблона

.. code-block:: protobuf

    message TemplateTransformationInfo
    {
        optional DocumentId TransformedToLetterId = 1;
        optional string Author = 2;
    }


- *TransformedToLetterId* - идентификаторы сообщения и документа, созданного на основе шаблона :doc:`DocumentId`.

- *Author* - ФИО пользователя, который создал документ из шаблона.