ResolutionDocflowV3
===================

.. code-block:: protobuf

    message ResolutionDocflowV3
    {
        required bool IsFinished = 1;
        required string ParentEntityId = 2;
        required ResolutionStatus ResolutionStatus = 3;
        optional string ResolutionEntityId = 4;
    }

Структура представляет статус согласования документа или запроса на аннулирование. Содержится в структуре :doc:`DocflowV3`.

- *IsFinished* - признак того, что согласование по документу/запросу на аннулирование завершен, т.е. не требует дальнейших действий.
- *ParentEnitytId* – идентификатор сущности, к которой относится согласование (сам документ либо запрос на аннулирование).
- :doc:`ResolutionStatus <ResolutionStatusDocflow>` – статус согласования документа
- *ResolutionEntityId* - идентификатор сущности по согласованию (запрос согласования или подписи, согласование, подписание основной или согласующей подписью, отказ в подписи).

Сущность, на которую ссылается *ResolutionEntityId*, следует искать, в зависимости от значения *ResolutionStatus*, по следующим правилам:

- если *ResolutionStatus* принимает одно из значений *ApprovementRequested*, *ApprovementSignatureRequested*, *PrimarySignatureRequested* или *ActionsRequested*, то *ResolutionEntityId* находится в коллекции *Requests* в структуре :doc:`ResolutionEntities <ResolutionEntitiesV3>`
- если *ResolutionStatus* равен *Approved* или *Disapproved*, то *ResolutionEntityId* находится в коллекции *Resolutions* в структуре :doc:`ResolutionEntities <ResolutionEntitiesV3>`
- если *ResolutionStatus* равен *SignatureRequestRejected*, то *ResolutionEntityId* находится в коллекции *SignatureDenials* в структуре :doc:`ResolutionEntities <ResolutionEntitiesV3>`
- если *ResolutionStatus* равен *SignedWithApprovingSignature*, то *ResolutionEntityId* находится в коллекции *ApprovementSignatures* в структуре :doc:`ResolutionEntities <ResolutionEntitiesV3>`
- если *ResolutionStatus* равен *SignedWithPrimarySignature*, то *ResolutionEntityId* указывает на структуру :doc:`SignatureV3 <SignatureV3>` внутри одного из нижепредставленных контрактов:

  * :doc:`SenderTitleDocflow <SenderTitleDocflow>` (если речь идет об исходящем документе)

  * :doc:`ParticipantResponseDocflow <ParticipantResponseDocflow>` (если документ находится у промежуточного или конечного получателя)

  * :doc:`RevocationRequestDocflow <RevocationDocflowV3>` (для инициатора аннулирования)

  * :doc:`RevocationResponseDocflow <RevocationDocflowV3>`

- если *ResolutionStatus* равен *PrimarySignatureRejected*, то *ResolutionEntityId* указывает на структуру :doc:`SignatureRejectionDocflow <SignatureRejectionDocflow>` внутри одного из нижепредставленных контрактов:

  * :doc:`ParticipantResponseDocflow <ParticipantResponseDocflow>` (если документ находится у промежуточного или конечного получателя)

  * :doc:`RevocationResponseDocflow <RevocationDocflowV3>`


Структура :doc:`ResolutionEntities <ResolutionEntitiesV3>` находится, в зависимости от значения *ParentEntityId*, в структуре :doc:`DocflowV3` или :doc:`RevocationDocflowV3`.

