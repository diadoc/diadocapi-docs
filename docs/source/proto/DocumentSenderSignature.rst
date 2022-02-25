DocumentSenderSignature
=======================

Структура ``DocumentSenderSignature`` предназначена для представления ЭП к документам отправляемого черновика:

.. code-block:: protobuf

    message DocumentSenderSignature {
        required string ParentEntityId = 1;
        optional bytes Signature = 2;
        optional bool SignWithTestSignature = 4 [default = false];
        optional string PatchedContentId = 5;
        optional PowerOfAttorneyToPost PowerOfAttorney = 6;
    }

- ``ParentEntityId`` — идентификатор подписываемых данных в отправляемом сообщении. Данный идентификатор должен соответствовать содержимому поля :doc:`Entity.EntityId <Entity message>` какой-либо из сущностей (:doc:`Entity <Entity message>`) модифицируемого черновика (:doc:`Message`).

	Набор сущностей в сообщении и их идентификаторы можно получить либо из результата вызова метода :doc:`../http/PostMessage`, с помощью которого создавался черновик, либо с помощью вызова метода :doc:`../http/GetMessage`.

- ``Signature`` — ЭП (в некоторых случаях может отсутствовать). Если ЭП присутствует, то она должна быть представлена в формате :rfc:`CMS SignedData <5652#section-5>` в `DER <http://www.itu.int/ITU-T/studygroups/com17/languages/X.690-0207.pdf>`__-кодировке.

- ``SignWithTestSignature`` — параметр, который позволяет запросить формирование тестовой ЭП под пересылаемыми данными.

- ``PatchedContentId`` — необязательный параметр, позволяющий задать идентификатор содержимого документа, подготовленного к подписанию с помощью метода :doc:`../http/PrepareDocumentsToSign`

- ``PowerOfAttorney`` — данные машиночитаемой доверенности, представленные структурой :doc:`PowerOfAttorneyToPost`.

----

.. rubric:: Использование

Структура ``DocumentSenderSignature`` используется внутри структуры :doc:`DraftToSend` при отправке документов методом :doc:`../http/SendDraft`.