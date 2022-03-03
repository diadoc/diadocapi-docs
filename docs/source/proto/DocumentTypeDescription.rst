DocumentTypeDescription
=======================

.. code-block:: protobuf

    message DocumentTypeDescription {
        required string Name = 1;
        required string Title = 2;
        repeated DocumentDocflow SupportedDocflows = 3;
        required bool RequiresFnsRegistration = 4;
        repeated DocumentFunction Functions = 9;
    }

    enum DocumentDocflow {
        External = 0;       // внешний документооборот
        Internal = 1;       // внутренний документооборот
    }

-  *Name* - уникальный строковой идентификатор типа (он же TypeNamedId в других контрактах и методах)
-  *Title* - заголовок типа, человеко-понятное название (например, "Счёт-фактура")
-  *SupportedDocflows* - поддерживаемые типы документооборота
-  *RequiresFnsRegistration* - для работы требуется заявление участника ЭДО
-  :ref:`Functions <document-function>` - описания функций документа

.. _document-function:

DocumentFunction
----------------

Описывает функцию документа.

.. code-block:: protobuf

    message DocumentFunction {
        required string Name = 1;
        repeated DocumentVersion Versions = 2;
    }

-  *Name* - строковой идентификатор функции, уникальное в рамках типа документов
-  :ref:`Versions <document-version>` - описания версий документа

.. _document-version:

DocumentVersion
~~~~~~~~~~~~~~~

Описывает версию документа.

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

-  *Version* - строковой идентификатор версии, уникальный в рамках функции документа
-  *SupportsContentPatching* - поддерживается патчинг
-  *SupportsEncrypting* - поддерживается отправка зашифрованных документов
-  *SupportsPredefinedRecipientTitle* - поддерживается отправка предопределенного титула. Подробнее здесь: :doc:`../howto/example_predefined_recipient_title`.
-  *SupportsAmendmentRequest* - поддерживается отправка запроса на уточнение.
-  :ref:`Titles <document_title>` - описания титулов документа
-  *IsActual* - версия актуальна
-  :doc:`Workflows <DocumentWorkflow>` - виды документооборота


.. _document_title:

DocumentTitle
`````````````

Описывает титул документа.

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

-  *Index* - числовой идентификатор титула. По смыслу означает, в каком порядке титулы загружаются контрагентами. Всегда начинается с 0.
-  *IsFormal* - титул формализованный
-  *XsdUrl* - URL-путь метода, возвращающего файл XSD-схемы титула
-  *UserDataXsdUrl* - URL-путь метода, возвращающего файл XSD-схемы контракта для генерации титула с помощью обобщённого метода генерации. Может отсутствовать, тогда это означает, что генерация титула под этим индексом нереализована. Для генерации титулов используется метод :doc:`GenerateTitleXml <../http/GenerateTitleXml>`.
-  :ref:`SignerInfo <signer-info>` - описание подписанта титула
-  :ref:`MetadataItems <document-metadata-item>` - описания метаданных документа
-  :ref:`EncryptedMetadataItems <document-metadata-item>` - описания метаданных для отправки зашифрованного документа

.. _signer-info:

SignerInfo
********************

Описывает тип подписанта титула.

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

-  *SignerType* - тип подписанта необходимый для титула

    -  *None* - подписант отсутствует в контенте документа. Формируется только файл открепленной подписи. Используется для неформализованных документов

    -  *Signer* - простой подписант. Используется для документов форматов :doc:`@93/@172 <../docflows/AttachmentVersion>` и своих типов документов не на базе формата :doc:`@155 <../docflows/AttachmentVersion>`

    -  *ExtendedSigner* - расширенный подписант. Используется для документов форматов :doc:`@155/@551/@552/@820 <../docflows/AttachmentVersion>` и своих типов на базе формата :doc:`@155 <../docflows/AttachmentVersion>`

-  :doc:`DocumentTitleType <DocumentTitleType>` - Тип титула документа, для которого нужно заполнить дополнительные данные о подписанте. Для типов подписанта *None* и *Signer* значение всегда равно *Absent*.

.. _document-metadata-item:

DocumentMetadataItem
********************

Описывает метаданные документа.

.. code-block:: protobuf

    message DocumentMetadataItem {
        required string Id = 1;
        required DocumentMetadataItemType Type = 2;
        required bool IsRequired = 3;
        required DocumentMetadataSource Source = 4;
    }

    enum DocumentMetadataItemType {
        String = 0;                     // строка
        Integer = 1;                    // целое число
        Decimal = 2;                    // число с десятичной точкой
        Date = 3;                       // дата в формате ДД.ММ.ГГГГ
        Time = 4;                       // время в формате чч:мм
    }

    enum DocumentMetadataSource {
        Xml = 0;                        // метаданные содержатся в теле документа
        User = 1;                       // метаданные передаются в метод API отдельными полями
    }

-  *Id* - идентификатор
-  *Type* - тип значения
-  *IsRequired* - обязательность
-  *Source* - способ передачи метаданных

