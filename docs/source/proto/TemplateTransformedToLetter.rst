TemplateTransformedToLetter
============================

Cодержит информацию о документе, созданном на основе шаблона.

.. code-block:: protobuf

    message TemplateTransformedToLetter
    {
        required string LetterFromBoxId = 1;
        required string LetterToBoxId = 2;
        optional string LetterFromDepartmentId = 3;		
        optional string LetterToDepartmentId = 4;
    }


- *LetterFromBoxId* - идентификатор ящика отправителя документа, созданного на основе шаблона.

- *LetterToBoxId* - идентификатор ящика получателя документа, созданного на основе шаблона.

- *LetterFromDepartmentId* - идентификатор подразделения отправителя документа, созданного на основе шаблона.

- *LetterToDepartmentId* - идентификатор подразделения получателя документа, созданного на основе шаблона.