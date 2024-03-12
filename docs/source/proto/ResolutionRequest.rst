ResolutionRequest
=================

На этой странице описаны следующие структуры:

.. contents:: :local:

.. _ResolutionRequestInfo:

ResolutionRequestInfo
---------------------

Структура ``ResolutionRequestInfo`` содержит информацию о состоянии запроса на согласование.

.. code-block:: protobuf

    message ResolutionRequestInfo {
        optional ResolutionRequestType Type = 1 [default = UnknownResolutionRequestType];
        required string Author = 2;
        optional ResolutionTarget Target = 3;
        optional string ResolvedWith = 4;
        repeated ResolutionAction Actions = 5;
    }

- ``Type`` — тип запроса на согласование, представленный структурой :ref:`ResolutionRequestType`.
- ``Author`` — ФИО инициатора запроса.
- ``ResolutionTarget`` — информация о том, кому направлен запрос.
- ``ResolvedWith`` — идентификатор ответного действия: положительное или отрицательное согласование, отказ в запросе подписи.
- ``Actions`` — действия, которые можно выполнить в рамках текущего запроса на согласование.

.. _ResolutionRequestType:

ResolutionRequestType
---------------------

Перечисление ``ResolutionRequestType`` представляет собой тип запроса на согласование документа.

.. code-block:: protobuf 

    enum ResolutionRequestType {
        UnknownResolutionRequestType = -1;
        ApprovementRequest = 0;
        SignatureRequest = 1;
        ApprovementSignatureRequest = 2;
        Custom = 3;
    }

- ``ApprovementRequest`` — запрос на согласование документа. В рамках запроса можно выполнитьодно из действий:

	- согласовать — ``ApproveAction``,
	- отказать в согласовании — ``DisapproveAction``.

- ``SignatureRequest`` — запрос на подпись документа. В рамках запроса можно выполнитьодно из действий:

	- подписать завершающей подписью — ``SignWithPrimarySignature``,
	- отказать в подписи контрагенту — ``RejectSigning``,
	- отказать в подписи сотруднику, запросившему подпись, — ``DenySignatureRequest``.

- ``ApprovementSignatureRequest`` — запрос на согласующую подпись под документом. В рамках типа запроса можно выполнить одно из действий:

	- подписать согласующей подписью — ``SignWithApprovementSignature``,
	- отказать в подписи сотруднику , запросившему подпись, — ``DenySignatureRequest``.

- ``Custom`` — запрос создан на основе шага маршрута согласования и не вписывается в стандартные типы.

Действия, которые можно выполнить по каждому из запросов на согласования, перечислены в поле ``Actions`` структуры :ref:`ResolutionRequestInfo`.

.. _ResolutionTarget:

ResolutionTarget
----------------

Структура ``ResolutionTarget`` содержит информацию о том, кому направлен запрос на согласование.

.. code-block:: protobuf

    message ResolutionTarget {
        optional string Department = 1;
        optional string DepartmentId = 2;
        optional string User = 3;
        optional string UserId = 4;
    }

- ``TargetDepartment`` — название подразделения, в которое направлен запрос.
- ``TargetDepartmentId`` — идентификатор подразделения, в которое направлен запрос.
- ``TargetUser`` — ФИО пользователя, которому направлен запрос.
- ``TargetUserId`` — идентификатор пользователя, которому направлен запрос.

Если запрос отправлен конкретному сотруднику, то будут заполены свойства ``User`` и ``UserId``, если в подразделение — ``Department`` и ``DepartmentId``.

.. _ResolutionAction:

ResolutionAction
----------------

Перечисление ``ResolutionAction`` описывает возможные действия по запросу на согласование.

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

- ``ApproveAction`` — согласовать.
- ``DisapproveAction`` — отказать в согласовании.
- ``SignWithApprovementSignature`` — подписать согласующей подписью.
- ``SignWithPrimarySignature`` — подписать завершающей подписью.
- ``DenySignatureRequest`` — отказать в подписи сотруднику.
- ``RejectSigning`` — отказать в подписи контрагенту.

ResolutionRequestAttachment
---------------------------

Структура ``ResolutionRequestAttachment`` содержит информацию для отправки запроса на согласование или подпись документа.

.. code-block:: protobuf

    message ResolutionRequestAttachment {
        required string InitialDocumentId = 1;
        required ResolutionRequestType Type = 2;
        optional string TargetUserId = 3;
        optional string TargetDepartmentId = 4;
        optional string Comment = 5;
        repeated string Labels = 6;
    }

- ``InitialDocumentId`` — идентификатор документа, для которого формируется запрос на согласование.
- ``ResolutionRequestType`` — тип запроса на согласование, представленный структурой :ref:`ResolutionRequestType`. Может принимать значения ``ApprovementRequest``, ``SignatureRequest`` и ``ApprovementSignatureRequest``.
- ``TargetUserId`` — идентификатор пользователя, которому будет направлен запрос на согласование.
- ``TargetDepartmentId`` — идентификатор подразделения, которому будет направлен запрос на согласование. Обязательно, если не заполнено ``TargetUserId``.
- ``Comment`` — комментарий к запросу согласования. Длина не должна превышать 500 символов.
- ``Labels`` — :doc:`метки <../proto/Labels>` запроса на согласование.

ResolutionRequestCancellationAttachment
---------------------------------------

Структура ``ResolutionRequestCancellationAttachment`` содержит информацию для отправки отмены запроса на согласование документа.

.. code-block:: protobuf

    message ResolutionRequestCancellationAttachment {
        required string InitialResolutionRequestId = 1;
        optional string Comment = 2;
        repeated string Labels = 3;
    }

- ``InitialResolutionRequestId`` — идентификатор отменяемого запроса на согласование.
- ``Comment`` — комментарий к отмене запроса на согласование. Длина не должна превышать 256 символов.
- ``Labels`` — :doc:`метки <../proto/Labels>` отмены запроса на согласование.
