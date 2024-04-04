ResolutionStatusDocflow
=======================

Перечисление ``ResolutionStatusDocflow`` представляет собой актуальный статус согласования документа/запроса на аннулирование.

.. code-block:: protobuf

    enum ResolutionStatus {
        UnknownStatus = 0;
        None = 1;
        Approved = 2;
        Disapproved = 3;
        ApprovementRequested = 4;
        ApprovementSignatureRequested = 5;
        PrimarySignatureRequested = 6;
        SignatureRequestRejected = 7;
        SignedWithApprovingSignature = 8;
        SignedWithPrimarySignature = 9;
        PrimarySignatureRejected = 10;
        ActionsRequested = 11;
    }

- ``UnknownStatus`` — возвращается для устаревших версий.
- ``None`` — нет активного согласования.
- ``Approved`` — документ или запрос на аннулирования согласован.
- ``Disapproved`` — отказано в согласовании документа или запроса на аннулирование.
- ``ApprovementRequested`` — запрошено согласование документа или запроса на аннулирование.
- ``ApprovementSignatureRequested`` — запрошена согласующая подпись под документом или запросом на аннулирование.
- ``PrimarySignatureRequested`` — запрошена основная подпись под документом или запросом на аннулирование.
- ``SignatureRequestRejected`` — отказано в подписи сотруднику.
- ``SignedWithApprovingSignature`` — документ или запрос на аннулирование подписан согласующей подписью.
- ``SignedWithPrimarySignature`` — документ или запрос на аннулирование подписан основной подписью.
- ``PrimarySignatureRejected`` — отказано контрагенту в основной подписи под документом или запросом на аннулировании.
- ``ActionsRequested`` — запрошено одно из действий в рамках запроса на согласование типа ``Custom``. Список действий представлен в поле :ref:`ResolutionRequestV3.Actions <ResolutionRequestV3>`.

----

.. rubric:: См. также

*Перечисление используется:*
	- в структуре :doc:`ResolutionDocflowV3`