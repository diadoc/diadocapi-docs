ResolutionAction
================

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

----

.. rubric:: См. также

*Перечисление используется:*
	- в структуре :doc:`ResolutionRequestInfo`
	- в структуре :ref:`ResolutionRequestV3`