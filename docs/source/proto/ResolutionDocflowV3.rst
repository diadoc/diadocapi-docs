ResolutionDocflowV3
===================

.. warning:: Эта версия контракта — экспериментальная и может измениться.

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

- если *ResolutionStatus* принимает одно из значений *ApprovementRequested*, *ApprovementSignatureRequested* или *PrimarySignatureRequested*, то *ResolutionEntityId* находится в коллекции *Requests* в структуре :doc:`ResolutionEntities <ResolutionEntitiesV3>`
- если *ResolutionStatus* равен *Approved* или *Disapproved*, то *ResolutionEntityId* находится в коллекции *Resolutions* в структуре :doc:`ResolutionEntities <ResolutionEntitiesV3>`
- если *ResolutionStatus* равен *SignatureRequestRejected*, то *ResolutionEntityId* находится в коллекции *SignatureDenials* в структуре :doc:`ResolutionEntities <ResolutionEntitiesV3>`
- если *ResolutionStatus* равен *SignedWithApprovingSignature*, то *ResolutionEntityId* находится в коллекции *ApprovementSignatures* в структуре :doc:`ResolutionEntities <ResolutionEntitiesV3>`
- если *ResolutionStatus* равен *SignedWithPrimarySignature*, то *ResolutionEntityId* указывает на структуру :doc:`SignatureV3 <SignatureV3>` либо внутри `SenderTitleDocflow` (если речь идет об исходящем документе), либо внутри `ProxyResponseDocflow` (если документ находится у промежуточного получателя), либо внутри `RecipientResponseDocflow` (для входящего документа), либо внутри `RevocationRequestDocflow` (для инициатора аннулирования), либо внутри `RevocationResponseDocflow`
- если *ResolutionStatus* равен *PrimarySignatureRejected*, то *ResolutionEntityId* указывает на структуру :doc:`SignatureRejectionDocflow <SignatureRejectionDocflow>` либо внутри `ProxyResponseDocflow` (если документ находится у промежуточного получателя), либо внутри `RecipientResponseDocflow` (для входящего документа), либо внутри `RevocationResponseDocflow`


Структура :doc:`ResolutionEntities <ResolutionEntitiesV3>` находится, в зависимости от значения *ParentEntityId*, в структуре :doc:`DocflowV3` или :doc:`RevocationDocflowV3`.

