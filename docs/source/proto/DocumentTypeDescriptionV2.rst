DocumentTypeDescriptionV2
=========================

Описывает тип документов. Возвращается методом :doc:`V2/GetDocumentTypes <../http/GetDocumentTypes>`.

.. code-block:: protobuf

    message DocumentTypeDescriptionV2 {
        required string Name = 1;
        required string Title = 2;
        repeated int32 SupportedDocflows = 3;
        required bool RequiresFnsRegistration = 4;
        repeated DocumentFunctionV2 Functions = 9;
    }

-  *Name* - уникальный строковой идентификатор типа (он же TypeNamedId в других контрактах и методах)
-  *Title* - заголовок типа, человеко-понятное название (например, "Счёт-фактура")
-  *SupportedDocflows* - поддерживаемые типы документооборота

    -  *0* - внешний документооборот

    -  *1* - внутренний документооборот

-  *RequiresFnsRegistration* - для работы требуется заявление участника ЭДО
-  :ref:`Functions <document-function>` - описания функций документа

.. _document-function:

DocumentFunctionV2
----------------

Описывает функцию документа.

.. code-block:: protobuf

    message DocumentFunctionV2 {
        required string Name = 1;
        repeated DocumentVersionV2 Versions = 2;
    }

-  *Name* - строковой идентификатор функции, уникальное в рамках типа документов
-  :ref:`Versions <document-version>` - описания версий документа

.. _document-version:

DocumentVersionV2
~~~~~~~~~~~~~~~

Описывает версию документа.

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

-  *Version* - строковой идентификатор версии, уникальный в рамках функции документа
-  *SupportsContentPatching* - поддерживается патчинг
-  *SupportsEncrypting* - поддерживается отправка зашифрованных документов
-  *SupportsPredefinedRecipientTitle* - поддерживается отправка предопределенного титула. Подробнее здесь: :doc:`../howto/example_predefined_recipient_title`.
-  *SupportsAmendmentRequest* - поддерживается отправка запроса на уточнение.
-  :ref:`Titles <document_title_v2>` - описания титулов документа
-  *IsActual* - версия актуальна
-  :doc:`Workflows <DocumentWorkflow>` - виды документооборота


.. _document-title_v2:

DocumentTitleV2
`````````````

Описывает титул документа.

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

-  *Index* - числовой идентификатор титула. По смыслу означает, в каком порядке титулы загружаются контрагентами. Всегда начинается с 0.
-  *IsFormal* - титул формализованный
-  *XsdUrl* - URL-путь метода, возвращающего файл XSD-схемы титула
-  *UserDataXsdUrl* - URL-путь метода, возвращающего файл XSD-схемы контракта для генерации титула с помощью обобщённого метода генерации. Может отсутствовать, тогда это означает, что генерация титула под этим индексом нереализована. Для генерации титулов используется метод :doc:`GenerateTitleXml <../http/GenerateTitleXml>`.
-  :ref:`SignerInfo <signer-info>` - описание подписанта титула
-  :ref:`MetadataItems <document-metadata-item>` - описания метаданных документа
-  :ref:`EncryptedMetadataItems <document-metadata-item>` - описания метаданных для отправки зашифрованного документа

.. _signer-info:

SignerInfoV2
********************

Описывает тип подписанта титула.

.. code-block:: protobuf

    message SignerInfoV2 {
        required int32 SignerType = 1;
        required int32 ExtendedDocumentTitleType = 2 [default = -1];
    }

-  *SignerType* - тип подписанта необходимый для титула

    -  *0* - подписант отсутствует в контенте документа. Формируется только файл открепленной подписи. Используется для неформализованных документов

    -  *1* - простой подписант. Используется для документов форматов :doc:`@93/@172 <../docflows/AttachmentVersion>` и своих типов документов не на базе формата :doc:`@155 <../docflows/AttachmentVersion>`

    -  *2* - расширенный подписант. Используется для документов форматов :doc:`@155/@551/@552/@820 <../docflows/AttachmentVersion>` и своих типов на базе формата :doc:`@155 <../docflows/AttachmentVersion>`

-  *ExtendedDocumentTitleType* - Тип титула документа, для которого нужно заполнить дополнительные данные о подписанте. Для типов подписанта *None* и *Signer* значение всегда равно -1.

    -  *0* - данные для титула продавца УПД

    -  *1* - данные для титула покупателя УПД

    -  *2* - данные для титула продавца УКД

    -  *3* - данные для титула покупателя УКД

    -  *4* - данные для титула продавца формата приказа 551

    -  *5* - данные для титула покупателя формата приказа 551

    -  *6* - данные для титула исполнителя формата приказа 552

    -  *7* - данные для титула для титула заказчика формата приказа 552

    -  *8* - данные для титула покупателя УПД формата приказа 820

    -  *9* - данные для титула покупателя Торг-2

    -  *10* - данные для титула продавца Торг-2
    
    -  *11* - данные для титула покупателя УКД формата приказа 736


.. _document-metadata-item:

DocumentMetadataItemV2
********************

Описывает метаданные документа.

.. code-block:: protobuf

    message DocumentMetadataItemV2 {
        required string Id = 1;
        required int32 Type = 2;
        required bool IsRequired = 3;
        required int32 Source = 4;
    }

-  *Id* - идентификатор
-  *IsRequired* - обязательность

*Type* - тип значения метаданных

-  *0* - строка

-  *1* - целое число

-  *2* - число с десятичной точкой

-  *3* - дата в формате ДД.ММ.ГГГГ

-  *4* - время в формате чч:мм

*Source* - способ передачи метаданных

-  *0* - метаданные содержатся в теле документа

-  *1* - метаданные передаются в метод API отдельными полями

