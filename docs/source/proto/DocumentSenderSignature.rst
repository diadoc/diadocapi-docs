DocumentSenderSignature
=======================

Структура ``DocumentSenderSignature`` представляет собой :doc:`электронную подпись <../entities/signature>` (ЭП) к данным в отправляемом черновике.

.. code-block:: protobuf

    message DocumentSenderSignature {
        required string ParentEntityId = 1;
        optional bytes Signature = 2;
        optional bool SignWithTestSignature = 4 [default = false];
        optional string PatchedContentId = 5;
        optional PowerOfAttorneyToPost PowerOfAttorney = 6;
    }

- ``ParentEntityId`` — идентификатор подписываемых данных в отправляемом сообщении. Должен соответствовать содержимому поля :doc:`Entity.EntityId <Entity message>` какой-либо :doc:`сущности <Entity message>` в модифицируемом черновике, представленном структурой :doc:`Message`.

  Набор сущностей в сообщении и их идентификаторы можно получить либо из результата вызова метода :doc:`../http/PostMessage`, с помощью которого создавался черновик, либо с помощью вызова метода :doc:`../http/GetMessage`.

- ``Signature`` — содержимое ЭП, представленное в формате :rfc:`CMS SignedData <5652#section-5>` в `DER <http://www.itu.int/ITU-T/studygroups/com17/languages/X.690-0207.pdf>`__-кодировке. В некоторых случаях может отсутствовать.

- ``SignWithTestSignature`` — флаг, который позволяет запросить формирование тестовой ЭП.

- ``PatchedContentId`` — идентификатор содержимого документа, :doc:`подготовленного к подписанию <../instructions/preparetosign>`. Должен быть получен методом :doc:`../http/PrepareDocumentsToSign`: идентификатор хранится в поле ``PatchedContentId`` структуры :doc:`PrepareDocumentsToSignResponse`.

- ``PowerOfAttorney`` — данные машиночитаемой доверенности, представленные структурой :doc:`PowerOfAttorneyToPost`.


----

.. rubric:: См. также

*Структура используется:*
	- в структуре :doc:`DraftToSend`

*Определение:*
	- :doc:`../entities/signature
	- :doc:`../entities/draft`