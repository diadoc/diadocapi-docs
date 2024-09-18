DocumentSignature
=================
  
Структура ``DocumentSignature`` представляет собой :doc:`электронную подпись <../entities/signature>` (ЭП) к данным в отправляемом сообщении.

.. code-block:: protobuf

    message DocumentSignature {
        required string ParentEntityId = 1;
        optional bytes Signature = 2;
        optional bool SignWithTestSignature = 4 [default = false];
        optional bool IsApprovementSignature = 5 [default = false];
        optional string SignatureNameOnShelf = 6;
        optional string PatchedContentId = 7;
        repeated string Labels = 8;
        optional PowerOfAttorneyToPost PowerOfAttorney = 9;
    }

- ``ParentEntityId`` — идентификатор подписываемых данных документа в отправляемом сообщении. Должен соответствовать содержимому поля :doc:`Entity.EntityId <Entity message>` какой-либо :doc:`сущности <Entity message>` в отправляемом сообщении :doc:`Message`. Набор сущностей в сообщении и их идентификаторы можно получить либо из результата вызова метода :doc:`../http/PostMessage` при создании сообщения, либо с помощью метода :doc:`../http/GetMessage`.

- ``Signature`` — содержимое ЭП, представленное в формате :rfc:`CMS SignedData <5652#section-5>` в `DER <http://www.itu.int/ITU-T/studygroups/com17/languages/X.690-0207.pdf>`__-кодировке. В некоторых случаях может отсутствовать.

- ``SignWithTestSignature`` — флаг, который позволяет запросить формирование тестовой ЭП.

- ``IsApprovementSignature`` — флаг, указывающий, что подпись является :ref:`согласующей <resolution_signature>`.

- ``SignatureNameOnShelf`` — имя подписи на :doc:`полке документов<../entities/shelf>`.

- ``PatchedContentId`` — идентификатор содержимого документа, :doc:`подготовленного к подписанию <../instructions/preparetosign>`. Должен быть получен методом :doc:`../http/PrepareDocumentsToSign` в поле ``PatchedContentId`` структуры :doc:`PrepareDocumentsToSignResponse`.

- ``Labels`` — :doc:`метки <../entities/label>` подписи.

- ``PowerOfAttorney`` — данные машиночитаемой доверенности, представленные структурой :doc:`PowerOfAttorneyToPost`.


----

.. rubric:: См. также

*Структура используется:*
	- в структуре :doc:`MessageToPost`

*Определение:*
	- :doc:`../entities/signature`