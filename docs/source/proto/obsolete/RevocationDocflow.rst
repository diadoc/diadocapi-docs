RevocationDocflow
=================

.. warning::
	Структура устарела. Вместо нее используется структура :doc:`../RevocationDocflowV3`.

Структура ``RevocationDocflow`` представляет информацию об аннулировании документа.

.. code-block:: protobuf

   message RevocationDocflow
   {
       optional bool IsFinished = 1;
       optional SignedAttachment RevocationRequestAttachment = 2;
       optional RecipientSignatureDocflow RecipientSignatureDocflow = 3;
       optional RecipientSignatureRejectionDocflow RecipientSignatureRejectionDocflow = 4;
       optional string InitiatorBoxId = 5;
       optional bool IsRevocationAccepted = 6;
       optional bool IsRevocationRejected = 7;
   }

- ``IsFinished`` — признак того, что документооборот завершен и документ не требует дальнейших действий.
- ``RevocationRequestAttachment`` — информация о файле предложения об аннулировании, представленная структурой :doc:`../SignedAttachment`.
- ``RecipientSignatureDocflow`` — информация об ответной подписи под предложением об аннулировании, представленная структурой :doc:`RecipientSignatureDocflow`.
- ``RecipientSignatureRejectionDocflow`` — информация об отказе в подписи предложения об аннулировании, представленная структурой :doc:`RecipientSignatureRejectionDocflow`.
- ``InitiatorBoxId`` — идентификатор ящика организации, которая инициировала аннулирование документа.
- ``IsRevocationAccepted`` — признак того, что запрос на аннулирование был одобрен.
- ``IsRevocationRejected`` — признак того, что запрос на аннулирование был отклонен.

----

.. rubric:: См. также

*Структура используется:*
	- в структуре :doc:`Docflow`