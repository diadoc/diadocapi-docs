ResolutionRequestType
=====================

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
	- ``DenySignatureRequest`` — отказать в подписи сотруднику, запросившему подпись.

- ``Custom`` — запрос создан на основе шага маршрута согласования и не вписывается в стандартные типы.

Действия, которые можно выполнить по каждому из запросов на согласование, перечислены в поле ``Actions`` структуры :doc:`ResolutionRequestInfo`.

----

.. rubric:: См. также

*Перечисление используется:*
	- в структуре :doc:`ResolutionRequestInfo`
	- в структуре :ref:`ResolutionRequestV3`