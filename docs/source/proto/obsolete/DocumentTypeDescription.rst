DocumentTypeDescription
=======================

.. warning::
	Структура устарела. Вместо нее используется структура :doc:`../DocumentTypeDescriptionV2`.

На этой странице, помимо ``DocumentTypeDescription``, описаны следующие структуры:

.. contents:: :local:


Структура ``DocumentTypeDescription`` хранит информацию о типе документов.

.. code-block:: protobuf

    message DocumentTypeDescription {
        required string Name = 1;
        required string Title = 2;
        repeated DocumentDocflow SupportedDocflows = 3;
        required bool RequiresFnsRegistration = 4;
        repeated DocumentFunction Functions = 9;
    }

    enum DocumentDocflow {
        External = 0;
        Internal = 1;
    }

- ``Name`` — строковый идентификатор типа документа.
- ``Title`` — заголовок типа документа, например, «Счет-фактура».
- ``SupportedDocflows`` — поддерживаемые типы документооборота. Каждый элемент списка принимает значение из перечисления ``DocumentDocflow``:

	- ``External`` — внешний документооборот;
	- ``Internal`` — внутренний документооборот.

- ``RequiresFnsRegistration`` — флаг, указывающий, что для работы требуется заявление участника ЭДО.
- ``Functions`` — список функций документа. Каждая функция представлена структурой :ref:`document-function`.


.. _document-function:

DocumentFunction
----------------

Структура ``DocumentFunction`` представляет собой функцию документа.

.. code-block:: protobuf

    message DocumentFunction {
        required string Name = 1;
        repeated DocumentVersion Versions = 2;
    }

- ``Name`` — строковой идентификатор функции. Уникальный в рамках типа документа.
- ``Versions`` — cписок версий документа. Каждая версия представлена структурой :ref:`document-version`.


.. _document-version:

DocumentVersion
---------------

Структура ``DocumentVersion`` представляет собой версию документа.

.. code-block:: protobuf

    message DocumentVersion {  
        required string Version = 1;
        required bool SupportsContentPatching = 2;
        required bool SupportsEncrypting = 3;        
        required bool SupportsPredefinedRecipientTitle = 7;
        required bool SupportsAmendmentRequest = 8;
        repeated DocumentTitle Titles = 4;
        required bool IsActual = 5;
        repeated DocumentWorkflow Workflows = 6;
    }

- ``Version`` — идентификатор версии. Уникальный в рамках функции документа.
- ``SupportsContentPatching``— флаг, указывающий, что тип поддерживает :doc:`подготовку к подписанию <../../instructions/preparetosign>` документа.
- ``SupportsEncrypting`` — флаг, указывающий, что тип поддерживает отправку зашифрованных документов.
- ``SupportsPredefinedRecipientTitle``— флаг, указывающий, что тип поддерживает отправкуа :doc:`предопределенного титула получателя <../../howto/example_predefined_recipient_title>`.
- ``SupportsAmendmentRequest``— флаг, указывающий, что тип поддерживает отправку запрос на уточнение.
- ``Titles`` — список титулов документов. Каждый титул представлен структурой :ref:`document-title`.
- ``IsActual`` — флаг, указывающий, что версия документа актуальна.
- ``Workflows`` — список видов документооборота для текущего типа. Каждый вид представлен структурой :doc:`../DocumentWorkflow`.


.. _document-title:

DocumentTitle
-------------

Структура ``DocumentTitle`` представляет собой титул документа.

.. code-block:: protobuf

    message DocumentTitle {
        required int32 Index = 7;
        required bool IsFormal = 1;
        optional string XsdUrl = 2;
        optional string UserDataXsdUrl = 5;
        required SignerInfo SignerInfo = 6;
        repeated DocumentMetadataItem MetadataItems = 3;
        repeated DocumentMetadataItem EncryptedMetadataItems = 4;
    }

- ``Index`` — числовой идентификатор титула. Указывает, в каком порядке контрагенты загружают титулы. Всегда начинается с 0.
- ``IsFormal`` — флаг, указывающий, что титул является формализованным.
- ``XsdUrl``— URL-путь метода, возвращающего файл XSD-схемы титула.
- ``UserDataXsdUrl`` — URL-путь метода, возвращающего XSD-схему ``UserDataXsd`` для генерации титула с помощью метода :doc:`../../http/GenerateTitleXml`. Если отсутствует, то генерация титула под этим индексом не реализована.
- ``SignerInfo`` — информация о подписанте титула, представленная структурой :ref:`signer-info`.
- ``MetadataItems`` — метаданные документа, представленные структурой :ref:`document-metadata-item`.
- ``EncryptedMetadataItems`` — метаданные зашифрованного документа, представленные структурой :ref:`document-metadata-item`.


.. _signer-info:

SignerInfo
----------

Структура ``SignerInfo`` представляет собой информацию о подписанте титула.

.. code-block:: protobuf

    message SignerInfo {
        required SignerType SignerType = 1;
        required DocumentTitleType ExtendedDocumentTitleType = 2 [default = Absent];
    }

    enum SignerType {
        None = 0;
        Signer = 1;
        ExtendedSigner = 2;
    }

- ``SignerType`` — тип подписанта титула. Принимает значение из перечисления ``SignerType``:

	- ``None`` — подписант отсутствует, формируется только файл открепленной подписи. Используется для неформализованных документов.
	- ``Signer`` — простой подписант. Используется для документов форматов :doc:`@93/@172 <../../docflows/AttachmentVersion>` и своих типов документов не на базе форматов :doc:`@155 <../../docflows/AttachmentVersion>`.
	- ``ExtendedSigner`` — расширенный подписант. Используется для документов форматов :doc:`@155//@551/@552/@820 <../../docflows/AttachmentVersion>` и своих типов документов на базе форматов :doc:`@155 <../../docflows/AttachmentVersion>`.

- ``ExtendedDocumentTitleType`` — тип титула документа, для которого нужно заполнить дополнительные данные о подписанте. Представлен структурой :doc:`../DocumentTitleType`. Для типов подписанта ``None`` и ``Signer`` значение всегда равно ``Absent``.


.. _document-metadata-item:

DocumentMetadataItem
--------------------

Структура ``DocumentMetadataItem`` представляет собой метаданные документа.

.. code-block:: protobuf

    message DocumentMetadataItem {
        required string Id = 1;
        required DocumentMetadataItemType Type = 2;
        required bool IsRequired = 3;
        required DocumentMetadataSource Source = 4;
    }

    enum DocumentMetadataItemType {
        String = 0;
        Integer = 1;
        Decimal = 2;
        Date = 3;
        Time = 4;
    }

    enum DocumentMetadataSource {
        Xml = 0;
        User = 1;
    }

- ``Id`` — идентификатор метаданных.
- ``Type`` — тип значения метаданных. Принимает значение из перечисления ``DocumentMetadataItemType``:

	- ``String`` — строка,
	- ``Integer`` — целое число,
	- ``Decimal`` — число с десятичной точкой,
	- ``Date`` — дата в формате ДД.ММ.ГГГГ,
	- ``Time`` — время в формате чч:мм.

- ``IsRequired`` — флаг, указывающий на обязательность заполнения поля метаданных.
- ``Source`` — источник метаданных. Принимает значение из перечисления ``DocumentMetadataSource``:

	- ``Xml`` — метаданные содержатся в теле документа;
	- ``User`` — метаданные передаются в метод API отдельными полями.