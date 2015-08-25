ResolutionRequest
=================

.. code-block:: protobuf

    message ResolutionRequestInfo {
        optional ResolutionRequestType RequestType = 1 [default = UnknownResolutionRequestType];
        required string Author = 2;
        optional ResolutionTarget Target = 3;
        optional string ResolvedWith = 4;
    }
    
    message ResolutionTarget {
    	optional string Department = 1;
    	optional string DepartmentId = 2;
    	optional string User = 3;
    	optional string UserId = 4;
    }

    enum ResolutionRequestType {
        UnknownResolutionRequestType = -1;
        ApprovementRequest = 0;
        SignatureRequest = 1;
        ApprovementSignatureRequest = 2;
    }

    message ResolutionRequestAttachment {
        required string InitialDocumentId = 1;
        required ResolutionRequestType Type = 2;
        optional string TargetUserId = 3;
        optional string TargetDepartmentId = 4;
        optional string Comment = 5;
    }

    message ResolutionRequestCancellationAttachment {
        required string InitialResolutionRequestId = 1;
    }
        

Структура данных *ResolutionRequestInfo* содержит информацию о состоянии запроса на согласование.

-  *ResolutionRequestType* - тип запроса на согласование:

   -  *ApprovementRequest* - запрос на согласование документа.

   -  *SignatureRequest* - запрос на подпись документа.
   
   -  *ApprovementSignatureRequest* - запрос на согласующую подпись под документом.

-  *Author* - ФИО инициатора запроса.

-  *ResolutionTarget* - информация о том, кому направлен запрос.

-  *ResolvedWith* - идентификатор ответного действия (положительное/отрицательное согласование, отказ в запросе подписи).


Структура данных *ResolutionRequestInfo* :

-  *TargetDepartment* - название подразделения, в которое направлен запрос.

-  *TargetDepartmentId* - идентификатор подразделения, в которое направлен запрос.

-  *TargetUser* - ФИО пользователя, которому направлен запрос.

-  *TargetUserId* - идентификатор пользователя, которому направлен запрос.


Структура данных *ResolutionRequestAttachment* содержит информацию для отправки запроса на согласование (или подпись) документа в методе :doc:`../http/PostMessagePatch`

-  *Type* - тип запроса на согласование.

-  *InitialDocumentId* - идентификатор документа, для которого формируется запрос на согласование.

-  *TargetUserId* - идентификатор пользователя, которому будет направлен запрос на согласование.

-  *TargetDepartmentId* - идентификатор подразделения, которому будет направлен запрос на согласование.

    Ровно одно из полей *TargetUserId* или *TargetDepartmentId* должно быть заполнено.

-  *Comment* - комментарий к запросу согласования.

Структура данных *ResolutionRequestCancellation* содержит информацию для отправки отмены запроса на согласование документа в методе :doc:`../http/PostMessagePatch`.

-  *InitialResolutionRequestId* - идентификатор отменяемого запроса на согласование.
