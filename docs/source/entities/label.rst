Метка (Label)
=============

К :doc:`служебным документам <../instructions/docservice>` в Диадоке можно добавить метки.

**Метка** — это строковый параметр, прикрепляемый к служебным документам и предназначенный для реализации логики их обработки. Метки могут помочь при реализации клиентской логики обработки служебных документов. Кроме этого в Диадоке есть предопределенные метки, которые влияют на поведение системы.

Метки, добавленные к сущности, хранятся в структуре :doc:`../proto/Entity message`. 

При документообороте метки передаются в ящик другой стороны вместе с документом.


Особенности и ограничения
-------------------------

- Длина метки должна быть не более 20 символов.
- Метка может содержать латинские буквы, цифры и дефисы.
- Только предопределенные метки могут начинаться с символа подчеркивания.
- Метки не регистрочувствительны.
- К одной сущности можно добавить не более 30 меток.
- К одной сущности нельзя добавить несколько одинаковых меток.


Предопределенные метки
----------------------

В Диадоке заведены следующие предопределенные метки:

- ``_impersonal`` — обезличенное действие. Если отправить извещение о получении :ref:`ReceiptAttachment` или уведомление об уточнении :ref:`CorrectionRequestAttachment` с этой меткой, то на странице документа в описании действия не будет упомянут сотрудник, который его совершил.


----

.. rubric:: См. также

*Метки используются:*
	- в структуре :ref:`CorrectionRequestAttachment`
	- в структуре :doc:`../proto/DocumentSignature`
	- в структуре :ref:`EditingPatch`
	- в структуре :doc:`../proto/Entity message`
	- в структуре :ref:`ReceiptAttachment`
	- в структуре :ref:`RecipientTitleAttachment`
	- в структуре :doc:`../proto/ResolutionAttachment`
	- в структуре :doc:`../proto/ResolutionRequestAttachment`
	- в структуре :doc:`../proto/ResolutionRequestCancellationAttachment`
	- в структуре :doc:`../proto/ResolutionRequestDenialAttachment`
	- в структуре :ref:`ResolutionRouteAssignment`
	- в структуре :ref:`ResolutionRouteRemoval`
	- в структуре :ref:`RequestedSignatureRejection`
	- в структуре :ref:`RevocationRequestAttachment`
	- в структуре :ref:`SignatureVerification`
	- в структуре :ref:`template-refusal-attachment`
	- в структуре :ref:`XmlSignatureRejectionAttachment`