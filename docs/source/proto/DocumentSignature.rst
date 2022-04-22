DocumentSignature
=================
  
Структура ``DocumentSignature`` предназначена для представления ЭП к некоторым данным в отправляемом сообщении:

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

- ``ParentEntityId`` — идентификатор подписываемых данных в отправляемом сообщении. Данный идентификатор должен соответствовать содержимому поля :doc:`Entity.EntityId <Entity message>` какой-либо из сущностей (:doc:`Entity <Entity message>`) модифицируемого отправляемого сообщения (:doc:`Message`).
   
   Набор сущностей в сообщении и их идентификаторы можно получить либо из результата вызова метода :doc:`../http/PostMessage`, с помощью которого создавалось сообщение, либо с помощью вызова метода :doc:`../http/GetMessage`

- ``Signature`` — ЭП (в некоторых случаях может отсутствовать). Если ЭП присутствует, то она должна быть представлена в формате :rfc:`CMS SignedData <5652#section-5>` в `DER <http://www.itu.int/ITU-T/studygroups/com17/languages/X.690-0207.pdf>`__-кодировке.

- ``SignWithTestSignature`` — параметр, который позволяет запросить формирование тестовой ЭП под пересылаемыми данными.

- ``IsApprovementSignature`` — является ли подпись согласующей или обычной.

- ``SignatureNameOnShelf`` — имя подписи на «полке документов».

- ``PatchedContentId`` — идентификатор патча документа

- ``Labels`` — :doc:`метки <../proto/Labels>` подписи.

- ``PowerOfAttorney`` — данные машиночитаемой доверенности, представленные структурой :doc:`PowerOfAttorneyToPost`.

Обычная подпись под документом может быть только одна с каждой стороны (отправителя или получателя), а согласующих подписей может быть сколько угодно.

Согласующие подписи можно ставить как со стороны отправителя, так и со стороны получателя, они проверяются и доставляются контрагенту.

Отличить полученную согласующую подпись от обычной можно по флажку ``IsApprovementSignature`` в структуре :doc:`Entity`.

Для неформализованного документа согласующую подпись можно ставить как до отправки документа, так и после. При этом, если поставить ее до отправки, то в ящик получателя она доставится только после отправки, вместе с документом и подписью отправителя.

Для формализованного документа согласующую подпись можно поставить только после отправки, потому что при отправке формализованного документа меняется его содержимое.

----

.. rubric:: Использование

Структура ``DocumentSignature`` используется внутри структуры :doc:`MessageToPost` при отправке документов методом :doc:`../http/PostMessagePatch`.