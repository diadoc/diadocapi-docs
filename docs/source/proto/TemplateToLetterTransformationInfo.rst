TemplateToLetterTransformationInfo
==================================

Cодержит информацию о документе, созданном на основе шаблона.

.. code-block:: protobuf

    message TemplateToLetterTransformationInfo
    {
        required string LetterFromBoxId = 1;
        required string LetterToBoxId = 2;
        optional string LetterFromDepartmentId = 3;		
        optional string LetterToDepartmentId = 4;
        optional string LetterProxyBoxId = 5;        
        optional string LetterProxyDepartmentId = 6; 
    }


- *LetterFromBoxId* - идентификатор ящика отправителя документа, созданного на основе шаблона.

- *LetterToBoxId* - идентификатор ящика получателя документа, созданного на основе шаблона.

- *LetterFromDepartmentId* - идентификатор подразделения отправителя документа, созданного на основе шаблона.

- *LetterToDepartmentId* - идентификатор подразделения получателя документа, созданного на основе шаблона.

- *LetterProxyBoxId* - идентификатор ящика промежуточного получателя документа, созданного на основе шаблонов.

- *LetterProxyDepartmentId* - идентификатор подразделения промежуточного получателя документа, которое будет создано на основе отправляемого шаблона.
