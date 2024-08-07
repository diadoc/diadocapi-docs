Подпись
=======

**Электронная подпись (ЭП)** — цифровой аналог рукописной подписи, который содержит информацию об авторе документа и подтверждает отсутствие изменений в документе после подписания. Электронная подпись формируется закрытым ключом, соответствующим сертификату, и средствами криптографической защиты информации.

Работа с подписью в Диадоке
---------------------------

С помощью API Диадока нельзя создать подпись для документа, так как для ее создания используется закрытый ключ, который нельзя передавать третьим лицам. Подпись нужно сгенерировать самостоятельно.

С документом и его подписью в Диадоке работают следующие методы:

	- метод отправки сообщения :doc:`../http/PostMessage`: передайте подпись в поле ``Signature`` структуры :doc:`../proto/SignedContent`;
	- метод отправки дополнения к сообщению :doc:`../http/PostMessagePatch`: передайте подпись в поле ``Signature`` структуры :doc:`../proto/DocumentSignature`;
	- метод отправки черновика :doc:`../http/SendDraft`: передайте подпись в поле ``Signature`` структуры :doc:`../proto/DocumentSenderSignature`.

Эти методы принимают файл подписи в формате :rfc:`CMS SignedData <5652#section-5>` в `DER <http://www.itu.int/ITU-T/studygroups/com17/languages/X.690-0207.pdf>`__-кодировке.

Под документом могут стоять следующие подписи:

	- подписи отправителя — для отправки документов, сохраненных без отправки,
	- подписи получателя — для двусторонних документов с запросом подписи,
	- согласующие подписи,
	- ответные подписи под запросом на аннулирование документа.


.. _resolution_signature:

Согласующая подпись
~~~~~~~~~~~~~~~~~~~

Диадок позволяет нескольким сотрудникам организации поставить свои подписи под одним документом. Такие подписи называются согласующими.

Согласующие подписи можно ставить как со стороны отправителя, так и со стороны получателя. В день под документом можно поставить не больше 500 согласующих подписей. Диадок проверит и доставит все подписи контрагенту.

Согласующую подпись можно поставить до или после отправки в зависимости от типа документа:

	- для неформализованного документа — до или после отправки. Если поставить согласующую подпись до отправки, то в ящик получателя она доставится только после отправки, вместе с документом и подписью отправителя. Если поставить согласующую подпись после отправки — получатель получит ее сразу.
	- для формализованного документа — только после отправки, потому что при отправке формализованного документа поле «Подписант» заполняется данными из сертификата и меняется содержимое документа.

Отправитель сразу получит все подписи получателя под документом.

Отправить запрос на подписание документа согласующей подписью можно с помощью метода :doc:`../http/PostMessagePatch`. Для этого заполните поле ``ResolutionRequests`` структуры :doc:`../proto/MessagePatchToPost`.

Подписать документ согласующей подписью можно с помощью метода :doc:`../http/PostMessagePatch`. Для этого передайте файл подписи в поле ``Signature`` структуры :doc:`../proto/DocumentSignature` и укажите флаг ``IsApprovementSignature = true``.

Определить, что подпись является согласующей, можно по флагу ``IsApprovementSignature`` в структуре :doc:`../proto/Entity message`.

Функциональность недоступна по умолчанию. Чтобы получить возможность использовать согласующую подпись, обратитесь к менеджеру или в `техническую поддержку <https://www.diadoc.ru/support>`__.


----

.. rubric:: Представление в API

В API подписи представлены структурами:

	- :doc:`../proto/DocumentSignature` —  представляет собой электронную подпись к данным в отправляемом сообщении
	- :doc:`../proto/DocumentSenderSignature` — представляет собой электронную подпись к данным в отправляемом черновике
	- :doc:`../proto/Signature` — хранит информацию об электронной подписи под документом
	- :doc:`../proto/SignatureV3` — хранит информацию об электронной подписи под документом

.. rubric:: См. также

*Методы для работы с подписями:*
	- :doc:`../http/GetSignatureInfo` — возвращает информацию о подписи и сертификате в сообщении

*Структуры для работы с подписями:*
	- :doc:`../proto/SignatureInfo` — хранит информацию о подписи и сертификате

