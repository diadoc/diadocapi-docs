SignatureV3
===========

Структура ``SignatureV3`` хранит информацию об :doc:`электронной подписи <../entities/signature>` под документом.

.. code-block:: protobuf

    message SignatureV3
    {
        required Entity Cms = 1;
        optional Entity CadesT = 2;
        required string SignerBoxId = 3;
        required string SignerDepartmentId = 4;
        required bool IsValid = 5;
        optional SignatureVerificationResult VerificationResult = 6;
        optional Timestamp DeliveredAt = 7;
        optional SignaturePowerOfAttorney PowerOfAttorney = 8;
        optional PowerOfAttorneyAttachmentStatus PowerOfAttorneyAttachmentStatus = 9;
    }

- ``Cms`` — информация о содержимом оригинальной подписи, представленная структурой :doc:`Entity`.
- ``CadesT`` — информация о содержимом подписи в формате CADES-T, представленная структурой :doc:`Entity`. 
- ``SignerBoxId`` — идентификатор ящика, от имени которого была поставлена подпись.
- ``SignerDepartmentId`` — идентификатор подразделения, сотрудник которого поставил подпись.
- ``IsValid`` — признак того, что подпись проверена и признана верной или еще не прошла проверку.
- ``VerificationResult`` — результат проверки подписи, представленный структурой :doc:`SignatureVerificationResult`. Возвращается в ответе методов, если в запросе был установлен флаг ``InjectEntityContent=true``.
- ``DeliveredAt`` — время доставки подписи, представленная структурой :doc:`Timestamp`.
- ``PowerOfAttorney`` — информация о машиночитаемой доверенности и ее статусе, представленная структурой :doc:`SignaturePowerOfAttorney`.
- ``PowerOfAttorneyAttachmentStatus`` — статус приложенности машиночитаемой доверенности к подписи, представленный структурой :doc:`PowerOfAttorneyAttachmentStatus`.


----

.. rubric:: См. также

*Определение:*
	- :doc:`../entities/signature`

*Структура используется:*
	- в структуре :doc:`ApprovementSignatureV3 <ResolutionEntitiesV3>`
	- в структуре :doc:`ParticipantResponseDocflow`
	- в структуре :doc:`RevocationResponseDocflow <RevocationDocflowV3>`
	- в структуре :doc:`SignedAttachmentV3`