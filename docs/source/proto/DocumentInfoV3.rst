DocumentInfoV3
==============

.. code-block:: protobuf

    message DocumentInfoV3
    {
        required FullVersion FullVersion = 1;
        required Documents.MessageType MessageType = 2;
        required int32 WorkflowId = 3;
        required DocumentParticipants Participants = 4;
        required DocumentDirection DocumentDirection = 5;
        required string DepartmentId = 6;
        optional string CustomDocumentId = 7;
        repeated Events.MetadataItem Metadata = 8;
        repeated CustomDataItem CustomData = 9;
        required DocumentLinks DocumentLinks = 10;
        required PacketInfo PacketInfo = 11;
        required bool IsRead = 12;
        required bool IsDeleted = 13;
        required bool IsInvitation = 14;
        optional DocumentLetterInfo LetterInfo = 15;
        optional DocumentDraftInfo DraftInfo = 16;
        optional DocumentTemplateInfo TemplateInfo = 17;
        optional Documents.Origin Origin = 18;
        optional string EditingSettingId = 19 [default = ""];
    }

Структура *DocumentInfoV3* представляет данные документа, которые не меняются в течение его жизненного цикла (метаданные). Как часть структуры :doc:`DocumentWithDocflowV3`, возвращается методами :doc:`../http/GetDocflows_V3`, :doc:`../http/GetDocflowsByPacketId_V3`, :doc:`../http/SearchDocflows_V3`.

- :doc:`FullVersion` - тип, функция и версия документа
- :doc:`MessageType` - тип сообщения: письмо, черновик или шаблон
- *WorkflowId* - :doc:`вид документооборота <DocumentWorkflow>`
- :doc:`Participants <DocumentParticipants>` - участники документооборота
- :doc:`DocumentDirection` - направление движения документа
- *DepartmentId* - идентификатор подразделения, в котором находится документ
- *CustomDocumentId* - идентификатор документа, определяемый внешней системой
- :doc:`Metadata <MetadataItem>` - метаданные документа
- :doc:`CustomData <CustomDataItem>` - пользовательские данные, привязанные к документу
- :doc:`DocumentLinks` - идентификаторы документов, на которые ссылается данный документ, и которые ссылаются на данный документ
- :doc:`PacketInfo` - информация о пакете, в котором содержится документ
- *IsRead* - был ли документ прочитан сотрудником организации
- *IsDeleted* - был ли удален данный документ
- *IsInvitation* - является ли документ приглашением к ЭДО (тип документа - TrustConnectionRequest, или он поддерживает работу в режиме приглашения и отправлен в таком режиме)
- :ref:`LetterInfo <document-letter-info>` - информация о письме, заполянется когда MessageType = Letter
- :ref:`DraftInfo <document-draft-info>` - информация о черновике, заполянется когда MessageType = Draft
- :ref:`TemplateInfo <document-template-info>` - информация о шаблоне, заполянется когда MessageType = Template
- :doc:`Origin` - ссылка на письмо, на основе которого был создан документ
- *EditingSettingId* - идентификатор настройки редактирования содержимого документа. Наличие настройки означает, что в содержимом файла может отсутствовать контент, редактирование которого разрешено этой настройкой.

.. _document-letter-info:

DocumentLetterInfo
------------------

.. code-block:: protobuf

    message DocumentLetterInfo
    {
        required bool IsEncrypted = 1;
        repeated ForwardDocumentEvent ForwardDocumentEvents = 2;
        required bool IsTest = 3;
    }

Структура содержит свойства, присущие только документам в письме.

- *IsEncrypted* - является ли документ зашифрованным
- :doc:`ForwardDocumentEvents <ForwardDocumentEvent>` - события пересылки документа третьим сторонам
- *IsTest* - является ли документ тестовым

.. _document-draft-info:

DocumentDraftInfo
-----------------

.. code-block:: protobuf

    message DocumentDraftInfo
    {
        required bool IsRecycled = 1;
        required bool IsLocked = 2;
        repeated string TransformedToLetterIds = 3;
    }

Структура содержит свойства, присущие только документам в черновике.

- *IsRecycled* - удален ли черновик
- *IsLocked* - залочен ли черновик
- *TransformedToLetterIds* - список идентификаторов писем, созданных на основе данного черновика

.. _document-template-info:

DocumentTemplateInfo
--------------------

.. code-block:: protobuf

    message DocumentTemplateInfo
    {
        required DocumentParticipants LetterParticipants = 1;
        repeated string TransformedToLetterIds = 2;
        repeated TemplateTransformationInfo TemplateTransformationInfos = 3;
        optional TemplateRefusalInfo TemplateRefusalInfo = 4;
        optional bool IsReusable = 5 [default = false];
    }

Структура содержит свойства, присущие только документам в шаблоне

- :doc:`LetterParticipants <DocumentParticipants>` - информация об отправителе и получателе письма, которое можно создать на основе данного шаблона
- :ref:`TemplateTransformationInfo <template-transformation-info>` - список идентификаторов писем, созданных на основе данного шаблона и содержащих данный документ
- :ref:`TemplateRefusalInfo <template-refusal-info>` - информация об отклонении или отзыве шаблона
- *IsReusable* - признак указывает на то, что шаблон может быть использован больше одного раза

.. _template-transformation-info:

TemplateTransformationInfo
~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: protobuf

    message TemplateTransformationInfo
    {
        required string TransformationId = 1;
        optional DocumentId TransformedToLetterId = 2;
        optional string AuthorUserId = 3;
    }

Структура содержит информацию о документе, созданном на основе шаблона.

- *TransformationId* - идентификатор трансформации
- :doc:`TransformedToLetterId <DocumentId>` - идентификаторы письма и документа, созданного на основе шаблона
- *AuthorUserId* - идентификатор пользователя, который создал документ из шаблона

.. _template-refusal-info:

TemplateRefusalInfo
~~~~~~~~~~~~~~~~~~~

.. code-block:: protobuf

    message TemplateRefusalInfo
    {
        required string BoxId = 1;
        optional string AuthorUserId = 2;
        optional string AuthorName = 3;
        optional string Comment = 4;
    }

Структура содержит информацию об отклонении или отзыве шаблона.

- *BoxId* - идентификатор ящика, на стороне которого выполнено отклонение или отзыв.
- *AuthorUserId* - идентификатор пользователя, который выполнил отклонение или отзыв.
- *AuthorName* - ФИО пользователя, который выполнил отклонение или отзыв.
- *Comment* - комментарий, который был указан при отклонении или отзыве.
