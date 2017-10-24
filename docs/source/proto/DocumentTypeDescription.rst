DocumentTypeDescription
=======================

Описывает тип документов. Возвращается методом :doc:`../http/GetDocumentTypes`.

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

-  *Name* - уникальный строковой идентификатор типа
-  *Title* - заголовок типа
-  *SupportedDocflows* - поддерживаемые типы документооборота
-  *RequiresFnsRegistration* - для работы требуется заявление участника ЭДО
-  *Functions* - описания функций документа

DocumentFunction
----------------

Описывает функцию документа.

.. code-block:: protobuf

    message DocumentFunction {
        required string Name = 1;
        repeated DocumentVersion Versions = 2;
        repeated DocumentWorkflow Workflows = 3;
    }

-  *Name* - строковой идентификатор функции, уникальное в рамках типа документов
-  *Versions* - описания версий документа
-  :doc:`Workflows <DocumentWorkflow>` - варианты документооборота

DocumentVersion
~~~~~~~~~~~~~~~

Описывает версию документа.

.. code-block:: protobuf

    message DocumentVersion {
        required string Version = 1;
        required bool SupportsContentPatching = 2;
        required bool SupportsEncrypting = 3;
        repeated DocumentTitle Titles = 4;
        required bool IsActual = 5;
    }

-  *Version* - строковой идентификатор версии, уникальный в рамках функции документа
-  *SupportsContentPatching* - поддерживается патчинг
-  *SupportsEncrypting* - поддерживается отправка зашифрованных документов
-  *Titles* - описания титулов документа
-  *IsActual* - версия актуальна

DocumentTitle
`````````````

Описывает титул документа.

.. code-block:: protobuf

    message DocumentTitle {
        required bool IsFormal = 1;
        optional string XsdUrl = 2;
        repeated DocumentMetadataItem MetadataItems = 3;
        repeated DocumentEncryptedMetadataItem EncryptedMetadataItems = 4;
    }

-  *IsFormal* - титул формализованный
-  *XsdUrl* - адрес метода, возвращающего файл XSD-схемы
-  *MetadataItems* - описания метаданных документа
-  *EncryptedMetadataItems* - описания метаданных, которые необходимо указать при отправке зашифрованного документа

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

-  *Id* - идентификатор
-  *Type* - тип значения
-  *IsRequired* - обязательность
-  *Source* - способ передачи метаданных

