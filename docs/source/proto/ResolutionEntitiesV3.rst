ResolutionEntitiesV3
====================

.. code-block:: protobuf

    message ResolutionEntitiesV3
    {
        repeated ResolutionRequestV3 Requests = 1;
        repeated ResolutionV3 Resolutions = 2;
        repeated ApprovementSignatureV3 ApprovementSignatures = 3;
        repeated SignatureDenialV3 SignatureDenials = 4;        
    }

В структуре `ResolutionEntitiesV3` собраны сущности, относящиеся к согласованию документа или запроса на аннулирование.

- *Requests* - содержит запросы на согласование/согласующую подпись/основную подпись;
- *Resolutions* - содержит согласования/отказы в согласовании;
- *ApprovementSignatures* - содержит согласующие подписи;
- *SignatureDenials* - содержит отказы в подписи сотруднику.

.. _ResolutionRequestV3:

ResolutionRequestV3
-------------------

.. code-block:: protobuf

    message ResolutionRequestV3
    {
        required Entity Entity = 1;
        required ResolutionTarget Target = 2;
        optional string AuthorUserId = 3;
        required ResolutionRequestType RequestType = 4;
        optional string ResolvedWith = 5; 
        repeated ResolutionAction Actions = 6;
    }

Структура `ResolutionRequestV3` описывает запрос на согласование документа или запроса на аннулирование

- :doc:`Entity <Entity>` - содержит информацию о содержимом запроса (идентификатор, время создания). В качестве содержимого запроса следует рассматривать комментарий к запросу;
- :ref:`Target <ResolutionTarget>` - информация о том, кому направлен запрос (пользователь или подразделение);
- *AuthorUserId* - идентификатор пользователя, запросившего согласование/подпись;
- :ref:`RequestType <ResolutionRequestType>` - тип запроса на согласование;
- *ResolvedWith* - идентификатор ответного действия (положительное/отрицательное согласование, отказ в запросе подписи сотруднику, подпись, отказ в подписи контрагенту).
- :ref:`Actions <ResolutionAction>` - действия, которые можно выполнить в рамках текущего запроса на согласование.

ResolutionV3
------------

.. code-block:: protobuf

    message ResolutionV3
    {
        required Entity Entity = 1;
        optional string ResolutionRequestId = 2;
        optional string AuthorUserId = 3;
        required ResolutionType ResolutionType = 4;
    }

Структура `ResolutionV3` описывает согласование документа или запроса на аннулирование

- :doc:`Entity <Entity>` - содержит информацию о согласовании (идентификатор, время создания). В качестве содержимого согласования следует рассматривать комментарий к согласованию/отказу;
- *ResolutionRequestId* - идентификатор запроса на согласование, если он был;
- *AuthorUserId* - идентификатор пользователя, совершившего согласование/отказ в согласовании;
- :ref:`ResolutionType` - тип действия по согласованию.

ApprovementSignatureV3
----------------------

.. code-block:: protobuf

    message ApprovementSignatureV3
    {
        required SignatureV3 Signature = 1;
        optional string ResolutionRequestId = 2;
        optional string AuthorUserId = 3;
    }

Структура `ApprovementSignatureV3` описывает согласующие подписи по документу или запросу на аннулирование

- :doc:`Signature <SignatureV3>` - данные о файле подписи
- *ResolutionRequestId* - идентификатор запроса согласующей подписи, если он был;
- *AuthorUserId* - идентификатор пользователя, совершившего согласование/отказ в согласовании.

SignatureDenialV3
-----------------

.. code-block:: protobuf

    message SignatureDenialV3
    {
        required Entity Entity = 1;
        required string ResolutionRequestId = 2;
        optional string AuthorUserId = 3;
    }

Структура `SignatureDenialV3` описывает отказ в подписи сотруднику

- :doc:`Entity <Entity>` - содержит информацию об отказе (идентификатор, время создания). В качестве содержимого октаза следует рассматривать комментарий к отказу;
- *ResolutionRequestId* - идентификатор запроса на согласование или подписи, если он был;
- *AuthorUserId* - идентификатор пользователя, совершившего согласование/отказ в согласовании.
