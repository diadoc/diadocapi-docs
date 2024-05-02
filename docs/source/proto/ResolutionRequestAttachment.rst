ResolutionRequestAttachment
===========================

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
- ``Type`` — тип запроса на согласование. Принимает следующие значения из перечисления :doc:`ResolutionRequestType`:

	- ``ApprovementRequest``,
	- ``SignatureRequest``,
	- ``ApprovementSignatureRequest``.

- ``TargetUserId`` — идентификатор пользователя, которому будет направлен запрос на согласование.
- ``TargetDepartmentId`` — идентификатор подразделения, в которое будет направлен запрос на согласование. Обязательно, если не заполнено ``TargetUserId``.
- ``Comment`` — комментарий к запросу согласования. Длина не должна превышать 500 символов.
- ``Labels`` — :doc:`метки <../proto/Labels>` запроса на согласование.

----

.. rubric:: См. также

*Структура используется:*
	- в структуре :doc:`MessagePatchToPost`