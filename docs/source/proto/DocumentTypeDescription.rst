DocumentTypeDescription
========================

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

Структура *DocumentTypeDescription*, возвращаемая методом :doc:`../http/GetDocumentTypes`, представляет описание типа документов.

-  *Name* - уникальный строковой идентификатор типа
-  *Title* - заголовок типа
-  *SupportedDocflows* - поддерживаемые типы документооборота
-  *RequiresFnsRegistration* - тип требует регистрации в ФНС
-  *Functions* - описания функций документа

DocumentFunction
----------------

.. code-block:: protobuf

    message DocumentFunction {
        required string Name = 1;
        repeated DocumentVersion Versions = 2;
        repeated DocumentWorkflow Workflows = 3;
    }

Структура *DocumentFunction* представляет описание функции документа.

-  *Name* - строковой идентификатор функции, уникальное в рамках типа документов
-  *Versions* - описания версий документа
-  :doc:`Workflows <DocumentWorkflow>` - варианты документооборота

DocumentVersion
~~~~~~~~~~~~~~~

.. code-block:: protobuf

    message DocumentVersion {
        required string Version = 1;
        required bool SupportsContentPatching = 2;
        required bool SupportsEncrypting = 3;
        repeated DocumentTitle Titles = 4;
        required bool IsActual = 5;
    }

Структура *DocumentVersion* представляет описание версии документа.

-  *Version* - строковой идентификатор версии, уникальный в рамках функции документа
-  *SupportsContentPatching* - поддерживается патчинг
-  *SupportsEncrypting* - поддерживается отправка зашифрованных документов
-  *Titles* - описания титулов документа
-  *IsActual* - версия актуальна

DocumentTitle
`````````````

.. code-block:: protobuf

    message DocumentTitle {
        required bool IsFormal = 1;
        optional string XsdUrl = 2;
        repeated DocumentMetadataItem MetadataItems = 3;
        repeated DocumentEncryptedMetadataItem EncryptedMetadataItems = 4;
    }

Структура *DocumentTitle* представляет описание титула документа.

-  *IsFormal* - титул формализованный
-  *XsdUrl* - адрес метода, возвращающего файл XSD-схемы
-  *MetadataItems* - описания метаданных документа
-  *EncryptedMetadataItems* - описания метаданных, которые необходимо указать при отправке зашифрованного документа

DocumentMetadataItem
********************

.. code-block:: protobuf

    message DocumentMetadataItem {
        required string Id = 1;
        required DocumentMetadataItemType Type = 2;
        required bool IsRequired = 3;
        required DocumentMetadataSource Source = 4;
    }

    message DocumentEncryptedMetadataItem {
        required string Id = 1;
        required DocumentMetadataItemType Type = 2;
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

Структура *DocumentMetadataItem* представляет описание метаданных документа.

-  *Id* - идентификатор
-  *Type* - тип значения
-  *IsRequired* - обязательность
-  *Source* - способ передачи метаданных

