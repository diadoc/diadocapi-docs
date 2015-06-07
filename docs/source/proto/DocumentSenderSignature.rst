DocumentSenderSignature
=======================

.. code-block:: protobuf

    message DocumentSenderSignature {
        required string ParentEntityId = 1;
        optional bytes Signature = 2;
        optional bool SignWithTestSignature = 4 [default = false];
        optional string PatchedContentId = 5;
    }
        

Структура данных DocumentSenderSignature служит для представления ЭЦП к документам отправляемого черновика:

-  ParentEntityId - идентификатор подписываемых данных в отправляемом сообщении. Данный идентификатор должен соответствовать содержимому поля :doc:`Entity.EntityId <Entity message>` какой-либо из сущностей (:doc:`Entity <Entity message>`) модифицируемого черновика (:doc:`Message`).

Набор сущностей в сообщении и их идентификаторы можно получить либо из результата вызова метода :doc:`../http/PostMessage`, с помощью которого создавался черновик, либо с помощью вызова метода :doc:`../http/GetMessage`.

-  Signature - ЭЦП (в некоторых случаях может отсутствовать). Если ЭЦП присутствует, то она должна быть представлена в формате :rfc:`CMS SignedData <5652#section-5>` в `DER <http://www.itu.int/ITU-T/studygroups/com17/languages/X.690-0207.pdf>`__-кодировке.

-  SignWithTestSignature - параметр, который позволяет запросить формирование тестовой ЭЦП под пересылаемыми данными.

-  PatchedContentId - необязательный параметр, позволяющий задать идентификатор содержимого документа, подготовленного к подписанию с помощью метода :doc:`../http/PrepareDocumentsToSign`