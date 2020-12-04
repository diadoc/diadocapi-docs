RevocationDocflowV3
===================

.. code-block:: protobuf

    message RevocationDocflowV3
    {
        required bool IsFinished = 1;
        required RevocationRequestDocflow RevocationRequest = 2;
        optional RevocationResponseDocflow RevocationResponse = 3;
        required string InitiatorBoxId = 4;
        required Documents.RevocationStatus RevocationStatus = 5;
        optional ResolutionEntitiesV3 ResolutionEntities = 6;
        repeated OuterDocflowEntities OuterDocflowEntities  = 7;
    }

Структура представляет информацию об аннулировании документа. Содержится в структуре :doc:`DocflowV3`.

- *IsFinished* - признак того, что документооборот по аннулированию завершен, т.е. не требует дальнейших действий.
- :ref:`RevocationRequest <revocation-request-docflow>` - информация о предложении об аннулировании.
- :ref:`RevocationResponse <revocation-response-docflow>` - информация об ответе на предложение аннулирования.
- *InitiatorBoxId* - идентификатор ящика организации, которая инициировала аннулирование документа.
- :doc:`RevocationStatus` - статус аннулирования документа.
- :doc:`ResolutionEntities <ResolutionEntitiesV3>` - информация о сущностях, относящихся к согласованию аннулирования.
- :doc:`OuterDocflowEntities <OuterDocflowEntities>` - информация о сущностях, относящихся к внешнему документообороту по аннулированию.

.. _revocation-request-docflow:

RevocationRequestDocflow
------------------------

.. warning:: Эта версия контракта — экспериментальная и может измениться.

.. code-block:: protobuf

    message RevocationRequestDocflow
    {
        required SignedAttachmentV3 RevocationRequest = 1;
        optional Timestamp SentAt = 2;
        optional Timestamp DeliveredAt = 3;
        optional RoamingNotification RoamingNotification = 4;
        optional string PlainText = 5;
    }

Структура содержит информацию о предложении об аннулировании документа.

- :doc:`RevocationRequest <SignedAttachmentV3>` - информация о файле предложения об аннулировании
- :doc:`SentAt <Timestamp>` - метка времени отправки предложения об аннулировании
- :doc:`DeliveredAt <Timestamp>` - метка времени доставки предложения об аннулировании в ящик контрагента
- :doc:`RoamingNotification` - данные о доставке предложения об аннулировании в роуминг
- *PlainText* - текст запроса аннулирования

.. _revocation-response-docflow:

RevocationResponseDocflow
-------------------------

.. warning:: Эта версия контракта — экспериментальная и может измениться.

.. code-block:: protobuf

    message RevocationResponseDocflow
    {
        optional SignatureV3 RecipientSignature = 1;
        optional SignatureRejectionDocflow SignatureRejection = 2;
    }

Структура содержит информацию об ответе на предложение об аннулировании документа.

- :doc:`RecipientSignature <SignatureV3>` - информация об ответной подписи под предложением об аннулировании
- :doc:`SignatureRejection <SignatureRejectionDocflow>` - информация об отказе в подписи предложения об аннулировании
