ResolutionRequest
=================

На этой странице описаны следующие структуры и перечисления:

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
- ``Target`` — информация о том, кому направлен запрос, представленная структурой :ref:`ResolutionTarget`.
- ``ResolvedWith`` — идентификатор ответного действия: положительное или отрицательное согласование, отказ в запросе подписи.
- ``Actions`` — список действий, которые можно выполнить в рамках текущего запроса на согласование. Каждый элмент списка представлен структурой :ref:`ResolutionAction`.

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

- ``UnknownResolutionRequestType`` — неизвестный тип. Возвращается в случае, если клиент использует устаревшую версию SDK и не может интерпретировать состояние согласования, переданное сервером.

- ``ApprovementRequest`` — запрос на согласование документа. В рамках запроса можно выполнить одно из действий:

	- ``ApproveAction`` — согласовать,
	- ``DisapproveAction`` — отказать в согласовании.

- ``SignatureRequest`` — запрос на подпись документа. В рамках запроса можно выполнить одно из действий:

	- ``SignWithPrimarySignature`` — подписать завершающей подписью,
	- ``RejectSigning`` — отказать в подписи контрагенту,
	- ``DenySignatureRequest`` — отказать в подписи сотруднику, запросившему подпись.

- ``ApprovementSignatureRequest`` — запрос на согласующую подпись под документом. В рамках типа запроса можно выполнить одно из действий:

	- ``SignWithApprovementSignature`` — подписать согласующей подписью,
	- ``DenySignatureRequest`` — отказать в подписи сотруднику , запросившему подпись.

- ``Custom`` — запрос создан на основе шага маршрута согласования и не вписывается в стандартные типы.

Действия, которые можно выполнить по каждому из запросов на согласование, перечислены в поле ``Actions`` структуры :ref:`ResolutionRequestInfo`.

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

- ``Department`` — название подразделения, в которое направлен запрос.
- ``DepartmentId`` — идентификатор подразделения, в которое направлен запрос.
- ``User`` — ФИО пользователя, которому направлен запрос.
- ``UserId`` — идентификатор пользователя, которому направлен запрос.

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

- ``UnknownAction`` — неизвестное действие. Возвращается в случае, если клиент использует устаревшую версию SDK и не может интерпретировать состояние согласования, переданное сервером.
- ``ApproveAction`` — согласовать.
- ``DisapproveAction`` — отказать в согласовании.
- ``SignWithApprovementSignature`` — подписать согласующей подписью.
- ``SignWithPrimarySignature`` — подписать завершающей подписью.
- ``DenySignatureRequest`` — отказать в подписи сотруднику.
- ``RejectSigning`` — отказать в подписи контрагенту.

.. _ResolutionRequestAttachment:

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
- ``Type`` — тип запроса на согласование. Принимает следующие значения из перечисления :ref:`ResolutionRequestType`:

	- ``ApprovementRequest``,
	- ``SignatureRequest``,
	- ``ApprovementSignatureRequest``.

- ``TargetUserId`` — идентификатор пользователя, которому будет направлен запрос на согласование.
- ``TargetDepartmentId`` — идентификатор подразделения, в которое будет направлен запрос на согласование. Обязательно, если не заполнено ``TargetUserId``.
- ``Comment`` — комментарий к запросу согласования. Длина не должна превышать 500 символов.
- ``Labels`` — :doc:`метки <../proto/Labels>` запроса на согласование.

.. _ResolutionRequestCancellationAttachment:

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
