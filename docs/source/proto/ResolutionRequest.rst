ResolutionRequest
=================

ResolutionRequestInfo
---------------------

.. code-block:: protobuf

    message ResolutionRequestInfo {
        optional ResolutionRequestType RequestType = 1 [default = UnknownResolutionRequestType];
        required string Author = 2;
        optional ResolutionTarget Target = 3;
        optional string ResolvedWith = 4;
        repeated ResolutionAction Actions = 5;
    }

Структура данных *ResolutionRequestInfo* содержит информацию о состоянии запроса на согласование и является частью структуры :doc:`Entity <Entity message>` в случае, когда сущность имеет тип *AttachmentType.ResolutionRequest*:

- *ResolutionRequestType* - тип запроса на согласование.

- *Author* - ФИО инициатора запроса.

- *ResolutionTarget* - информация о том, кому направлен запрос.

- *ResolvedWith* - идентификатор ответного действия (положительное/отрицательное согласование, отказ в запросе подписи).

- *Actions* - действия, которые можно выполнить в рамках текущего запроса на согласование.

.. _ResolutionRequestType:

ResolutionRequestType
---------------------

.. code-block:: protobuf

    enum ResolutionRequestType {
        UnknownResolutionRequestType = -1;
        ApprovementRequest = 0;
        SignatureRequest = 1;
        ApprovementSignatureRequest = 2;
        Custom = 3;
    }

Структура определяет тип запроса на согласования документа:

- *ApprovementRequest* - запрос на согласование документа. Подразумевает два возможных действия --- Согласовать (*ApproveAction*) или Отказать в согласовании (*DisapproveAction*).

- *SignatureRequest* - запрос на подпись документа. В рамках запроса можно выполнить три действия --- Подписать завершающей подписью (*SignWithPrimarySignature*)/Отказать в подписи контрагенту (*RejectSigning*) или Отказать в подписи сотруднику (*DenySignatureRequest*), который запросил подпись.

- *ApprovementSignatureRequest* - запрос на согласующую подпись под документом. В рамках данного типа запроса можно либо Подписать согласующей подписью (*SignWithApprovementSignature*), либо Отказать в подписи сотруднику (*DenySignatureRequest*), который запросил подпись.

- *Custom* - запрос был создан на основе шага маршрута согласования и не вписывается в стандартные типы.

Действия, которые можно выполнить по каждому из запросов на согласования, перечислены в свойстве `Actions`.

.. _ResolutionTarget:

ResolutionTarget
----------------

.. code-block:: protobuf

    message ResolutionTarget {
    	optional string Department = 1;
    	optional string DepartmentId = 2;
    	optional string User = 3;
    	optional string UserId = 4;
    }

Структура содержит информацию о том, кому направлен запрос на согласование:

- *TargetDepartment* - название подразделения, в которое направлен запрос.

- *TargetDepartmentId* - идентификатор подразделения, в которое направлен запрос.

- *TargetUser* - ФИО пользователя, которому направлен запрос.

- *TargetUserId* - идентификатор пользователя, которому направлен запрос.

Если запрос назначен на конкретного сотрудника, то будут заполены свойства *User* и *UserId*. Если на подразделение, то --- *Department* и *DepartmentId*.

.. _ResolutionAction:

ResolutionAction
----------------

.. code-block:: protobuf

    enum ResolutionAction {
        UnknownAction = 0;
        ApproveAction = 1;
        DisapproveAction = 2;
        SignWithApprovementSignature = 3;
        SignWithPrimarySignature = 4;
        DenySignatureRequest = 5;
        RejectSigning = 6;
    }

Перечисление описывает возможные действия по запросу на согласование:

- *ApproveAction* - согласовать;

- *DisapproveAction* - отказать в согласовании;

- *SignWithApprovementSignature* - подписать согласующей подписью;

- *SignWithPrimarySignature* - подписать завершающей подписью;

- *DenySignatureRequest* - отказать в подписи сотруднику;

- *RejectSigning* - отказать в подписи контрагенту.

ResolutionRequestAttachment
---------------------------

.. code-block:: protobuf

    message ResolutionRequestAttachment {
        required string InitialDocumentId = 1;
        required ResolutionRequestType Type = 2;
        optional string TargetUserId = 3;
        optional string TargetDepartmentId = 4;
        optional string Comment = 5;
        repeated string Labels = 6;
    }

Структура данных *ResolutionRequestAttachment* содержит информацию для отправки запроса на согласование (или подпись) документа в методе :doc:`../http/PostMessagePatch`

- :ref:`Type <ResolutionRequestType>` - тип запроса на согласование. Допустимые значения --- *ApprovementRequest*, *SignatureRequest* и *ApprovementSignatureRequest*.

-  *InitialDocumentId* - идентификатор документа, для которого формируется запрос на согласование.

-  *TargetUserId* - идентификатор пользователя, которому будет направлен запрос на согласование.

-  *TargetDepartmentId* - идентификатор подразделения, которому будет направлен запрос на согласование.

    Ровно одно из полей *TargetUserId* или *TargetDepartmentId* должно быть заполнено.

-  *Comment* - комментарий к запросу согласования. Максимально допустимая длина - 500 символов.

-  *Labels* - :doc:`метки <../proto/Labels>` запроса на согласование.

ResolutionRequestCancellationAttachment
---------------------------------------

.. code-block:: protobuf

    message ResolutionRequestCancellationAttachment {
        required string InitialResolutionRequestId = 1;
        optional string Comment = 2;
        repeated string Labels = 3;
    }

Структура данных *ResolutionRequestCancellationAttachment* содержит информацию для отправки отмены запроса на согласование документа в методе :doc:`../http/PostMessagePatch`.

-  *InitialResolutionRequestId* - идентификатор отменяемого запроса на согласование.

-  *Comment* - комментарий к отмене запроса на согласование. Максимально допустимая длина - 256 символов.

-  *Labels* - :doc:`метки <../proto/Labels>` отмены запроса на согласование.
