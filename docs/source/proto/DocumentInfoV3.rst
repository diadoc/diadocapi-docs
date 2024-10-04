DocumentInfoV3
==============

Структура ``DocumentInfoV3`` представляет собой метаданные документа, которые не меняются в течение его жизненного цикла. 

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

    message DocumentLetterInfo
    {
        required bool IsEncrypted = 1;
        repeated ForwardDocumentEvent ForwardDocumentEvents = 2;
        required bool IsTest = 3;
    }

    message DocumentDraftInfo
    {
        required bool IsRecycled = 1;
        required bool IsLocked = 2;
        repeated string TransformedToLetterIds = 3;
    }

    message DocumentTemplateInfo
    {
        required DocumentParticipants LetterParticipants = 1;
        repeated string TransformedToLetterIds = 2;
        repeated TemplateTransformationInfo TemplateTransformationInfos = 3;
        optional TemplateRefusalInfo TemplateRefusalInfo = 4;
        optional bool IsReusable = 5 [default = false];
    }

    message TemplateTransformationInfo
    {
        required string TransformationId = 1;
        optional DocumentId TransformedToLetterId = 2;
        optional string AuthorUserId = 3;
    }

    message TemplateRefusalInfo
    {
        required string BoxId = 1;
        optional string AuthorUserId = 2;
        optional string Comment = 3;
    }

- ``FullVersion`` — тип, функция и версия документа, представленные структурой :doc:`FullVersion`.
- ``MessageType`` — тип сообщения, представленный структурой :doc:`MessageType`.  
- ``WorkflowId`` —  идентификатор :doc:`вида документооборота <../docflows/Workflows>`.
- ``Participants`` — участники документооборота, представленные структурой :doc:`DocumentParticipants`.
- ``DocumentDirection`` — направление движения документа, представленное структурой :doc:`DocumentDirection`.
- ``DepartmentId`` — идентификатор подразделения, в котором находится документ.
- ``CustomDocumentId`` — идентификатор документа во внешней системе.
- ``Metadata`` — список метаданных документа, представленных структурой :doc:`MetadataItem`.
- ``CustomData`` — список пользовательских данных (:doc:`тегов <../entities/tag>`), привязанных к документу, представленных структурой :doc:`CustomDataItem`.
- ``DocumentLinks`` — идентификаторы документов, на которые ссылается этот документ, и которые ссылаются на этот документ, представленные структурой :doc:`DocumentLinks`.
- ``PacketInfo`` — информация о пакете, в котором содержится документ, представленная структурой :doc:`PacketInfo`.
- ``IsRead`` — флаг, указывающий, что документ был прочитан сотрудником организации.
- ``IsDeleted`` — флаг, указывающий, что документ был удален.
- ``IsInvitation`` — флаг, указывающий, что документ является приглашением к ЭДО (тип документа — ``TrustConnectionRequest``, или он поддерживает работу в режиме приглашения и отправлен в таком режиме).
- ``LetterInfo`` — информация о письме. Заполняется, если ``MessageType = Letter``. Представлена структурой ``DocumentLetterInfo`` с полями:

	- ``IsEncrypted`` — флаг, указывающий, что документ передается в зашифрованном виде.
	- ``ForwardDocumentEvents`` — список событий пересылки документа третьим сторонам, представленных структурой :doc:`ForwardDocumentEvent`.
	- ``IsTest`` — флаг, указывающий, что документ является тестовым.

- ``DraftInfo`` — информация о черновике. Заполняется, если ``MessageType = Draft``. Представлена структурой ``DocumentDraftInfo`` с полями:

	- ``IsRecycled`` — флаг, указывающий, что черновик удален.
	- ``IsLocked`` — флаг, указывающий, что черновик заблокирован.
	- ``TransformedToLetterIds`` — список идентификаторов писем, созданных на основе данного черновика.

- ``TemplateInfo`` — информация о шаблоне. Заполняется, если ``MessageType = Template``. Представлена структурой ``DocumentTemplateInfo`` с полями:

	- ``LetterParticipants`` — информация об отправителе и получателе письма, которое можно создать на основе шаблона. Представлена структурой :doc:`DocumentParticipants`.
	- ``TemplateTransformationInfos`` — список идентификаторов писем, созданных на основе шаблона и содержащих данный документ. Представлены структурой ``TemplateTransformationInfo`` с полями:

		- ``TransformationId`` — идентификатор преобразования из шаблона.
		- ``TransformedToLetterId`` — список идентификаторов письма и документа, созданных на основе шаблона. Представлены структурой :doc:`DocumentId`.
		- ``AuthorUserId`` — идентификатор пользователя, создавшего документ из шаблона.

	- ``TemplateRefusalInfo`` — информация об отклонение или отзыве шаблона, представленная структурой ``TemplateRefusalInfo`` с полями:

		- ``BoxId`` — идентификатор ящика организации, на стороне которого шаблон отклонили или отозвали.
		- ``AuthorUserId`` — идентификатор пользователя, отклонившего или отозвавшего шаблон.
		- ``Comment`` — комментарий, указанный при отклонении или отзыве.

	- ``IsReusable`` — флаг, указывающий, что из шаблона можно создать больше одного документа.

- ``Origin`` — ссылка на письмо, на основе которого был создан документ, представленная структурой :doc:`Origin`.
- ``EditingSettingId`` — идентификатор :doc:`настройки редактирования <../instructions/editingsettings>` содержимого документа.


----

.. rubric:: См. также

*Структура используется:*
	- в структуре :doc:`DocumentWithDocflowV3`