DocumentTypeDescriptionV2
=========================

Структура ``DocumentTypeDescriptionV2`` хранит информацию о типе документов.

.. code-block:: protobuf

    message DocumentTypeDescriptionV2 {
        required string Name = 1;
        required string Title = 2;
        repeated int32 SupportedDocflows = 3;
        required bool RequiresFnsRegistration = 4;
        repeated DocumentFunctionV2 Functions = 9;
    }

- ``Name`` — идентификатор типа документа.
- ``Title`` — заголовок типа документа, например, "Счёт-фактура".
- ``SupportedDocflows`` — поддерживаемые типы документооборота.

	- 0 — внешний документооборот;

	- 1 — внутренний документооборот.

- ``RequiresFnsRegistration`` — флаг, указывающий, что для работы требуется заявление участника ЭДО.
- ``Functions`` — список функций документа. Каждая функция представлена структурой :ref:`DocumentFunctionV2 <document-function2>`.

.. _document-function2:

DocumentFunctionV2
------------------

Структура ``DocumentFunctionV2`` представляет собой функцию документа.

.. code-block:: protobuf

    message DocumentFunctionV2 {
        required string Name = 1;
        repeated DocumentVersionV2 Versions = 2;
    }

- ``Name`` — строковой идентификатор функции. Уникальный в рамках типа документа.
- ``Versions`` — cписок версий документа. Каждая версия представлена структурой :ref:`DocumentVersionV2 <document-version2>`.

.. _document-version2:

DocumentVersionV2
~~~~~~~~~~~~~~~~~

Структура ``DocumentVersionV2`` представляет собой версию документа.

.. code-block:: protobuf

    message DocumentVersionV2 {  
        required string Version = 1;
        required bool SupportsContentPatching = 2;
        required bool SupportsEncrypting = 3;        
        required bool SupportsPredefinedRecipientTitle = 7;
        required bool SupportsAmendmentRequest = 8;
        repeated DocumentTitleV2 Titles = 4;
        required bool IsActual = 5;
        repeated DocumentWorkflowV2 Workflows = 6;
    }

- ``Version`` — идентификатор версии. Уникальный в рамках функции документа.
- ``SupportsContentPatching``— флаг, указывающий, что поддерживается патчинг документа.
- ``SupportsEncrypting`` — флаг, указывающий, что можно отправлять зашифрованные документы.
- ``SupportsPredefinedRecipientTitle``— флаг, указывающий, что поддерживается отправка :doc:`предопределенного титула получателя <../howto/example_predefined_recipient_title>`.
- ``SupportsAmendmentRequest``— флаг, указывающий, что можно отправлять запрос на уточнение.
- ``Titles`` — список титулов документов. Каждый титул представлен структурой :ref:`DocumentTitleV2 <document-title_v2>`.
- ``IsActual`` — флаг, указывающий, что версия документа актуальна.
- ``Workflows`` — список видов документооборота. Каждый вид представлен структурой :doc:`DocumentWorkflow`.


.. _document-title_v2:

DocumentTitleV2
```````````````

Структура ``DocumentTitleV2`` представляет собой титул документа.

.. code-block:: protobuf

    message DocumentTitleV2 {
        required int32 Index = 7;
        required bool IsFormal = 1;
        optional string XsdUrl = 2;
        optional string UserDataXsdUrl = 5;
        required SignerInfoV2 SignerInfo = 6;
        repeated DocumentMetadataItemV2 MetadataItems = 3;
        repeated DocumentMetadataItemV2 EncryptedMetadataItems = 4;
    }

- ``Index`` — числовой идентификатор титула. Указывает, в каком порядке контрагенты загружают титулы. Всегда начинается с 0.
- ``IsFormal`` — флаг, указывающий, что титул является формализованным.
- ``XsdUrl``— URL-путь метода, возвращающего файл XSD-схемы титула.
- ``UserDataXsdUrl`` — URL-путь метода, возвращающего файл XSD-схемы контракта для генерации титула с помощью обобщённого метода генерации. Если отсутствует, то генерация титула под этим индексом не реализована. Для генерации титулов используйте метод :doc:`GenerateTitleXml <../http/GenerateTitleXml>`.
- ``SignerInfo`` — описание подписанта титула. Представлено структурой :ref:`SignerInfoV2 <signer-info2>`.
- ``MetadataItems`` — описания метаданных документа. Представлены структурой :ref:`DocumentMetadataItemV2 <document-metadata-item2>`.
- ``EncryptedMetadataItems`` — описания метаданных для отправки зашифрованного документа. Представлены структурой :ref:`DocumentMetadataItemV2 <document-metadata-item2>`.

.. _signer-info2:

SignerInfoV2
************

Структура ``SignerInfoV2`` представляет собой тип подписанта титула.

.. code-block:: protobuf

    message SignerInfoV2 {
        required int32 SignerType = 1;
        required int32 ExtendedDocumentTitleType = 2 [default = -1];
        optional string SignerUserDataXsdUrl = 3;
    }

- ``SignerType`` — тип подписанта титула.

	- 0 — подписант отсутствует. Формируется только файл открепленной подписи. Используется для неформализованных документов.

	- 1 — простой подписант. Используется для документов форматов :doc:`@93/@172 <../docflows/AttachmentVersion>` и своих типов документов не на базе форматов :doc:`@155/@820 <../docflows/AttachmentVersion>`.

	- 2 — расширенный подписант. Используется для документов форматов :doc:`@155/@189/@551/@552/@736/@820 <../docflows/AttachmentVersion>` и своих типов на базе форматов :doc:`@155/@820 <../docflows/AttachmentVersion>`

	- 3 — универсальный подписант. Используется, если заполнено поле ``SignerUserDataXsdUrl``.

- ``ExtendedDocumentTitleType`` — тип титула документа, для которого нужно заполнить дополнительные данные о подписанте.

	- -1 — указывается для типов подписанта 0, 1 или 3;

	- 0 — данные для титула продавца УПД;

	- 1 — данные для титула покупателя УПД;

	- 2 — данные для титула продавца УКД;

	- 3 — данные для титула покупателя УКД;

	- 4 — данные для титула продавца формата приказа 551;

	- 5 — данные для титула покупателя формата приказа 551;

	- 6 — данные для титула исполнителя формата приказа 552;

	- 7 — данные для титула для титула заказчика формата приказа 552;

	- 8 — данные для титула покупателя УПД формата приказа 820;

	- 9 — данные для титула покупателя Торг-2;

	- 10 - данные для титула продавца Торг-2;

	- 11 — данные для титула покупателя УКД формата приказа 736.

- ``SignerUserDataXsdUrl`` — URL-путь метода, возвращающего файл XSD-схемы упрощённого XML подписанта.

.. _document-metadata-item2:

DocumentMetadataItemV2
**********************

Структура ``DocumentMetadataItemV2`` представляет собой метаданные документа.

.. code-block:: protobuf

    message DocumentMetadataItemV2 {
        required string Id = 1;
        required int32 Type = 2;
        required bool IsRequired = 3;
        required int32 Source = 4;
    }

- ``Id`` — идентификатор метаданных.
- ``IsRequired`` — флаг, указывающий на обязательность заполнения поля метаданных.
- ``Type`` — тип значения метаданных.

	- 0 — строка;

	- 1 — целое число;

	- 2 — число с десятичной точкой;

	- 3 — дата в формате ДД.ММ.ГГГГ;

	- 4 — время в формате чч:мм.

- ``Source`` — способ передачи метаданных.

	- 0 — содержатся в теле документа;

	- 1 — передаются в метод API отдельными полями.

----

.. rubric:: Смотри также

*Структура используется:*
	- в теле ответа метода :doc:`../http/GetDocumentTypes`.
