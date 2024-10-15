﻿DocumentTypeDescriptionV2
=========================

На этой странице, помимо ``DocumentTypeDescriptionV2``, описаны следующие структуры:

.. contents:: :local:


Структура ``DocumentTypeDescriptionV2`` хранит информацию о типе документов.

.. code-block:: protobuf

    message DocumentTypeDescriptionV2 {
        required string Name = 1;
        required string Title = 2;
        repeated int32 SupportedDocflows = 3;
        required bool RequiresFnsRegistration = 4;
        repeated DocumentFunctionV2 Functions = 9;
    }

- ``Name`` — строковый идентификатор типа документа.
- ``Title`` — заголовок типа документа, например, «Счет-фактура».
- ``SupportedDocflows`` — поддерживаемые типы документооборота. Каждый элемент списка может принимать одно из значений:

	- 0 — внешний документооборот;
	- 1 — внутренний документооборот.

- ``RequiresFnsRegistration`` — флаг, указывающий, что для работы требуется заявление участника ЭДО.
- ``Functions`` — список функций документа. Каждая функция представлена структурой :ref:`DocumentFunctionV2`.


.. _DocumentFunctionV2:

DocumentFunctionV2
------------------

Структура ``DocumentFunctionV2`` представляет собой функцию документа.

.. code-block:: protobuf

    message DocumentFunctionV2 {
        required string Name = 1;
        repeated DocumentVersionV2 Versions = 2;
    }

- ``Name`` — строковой идентификатор функции. Уникальный в рамках типа документа.
- ``Versions`` — cписок версий документа. Каждая версия представлена структурой :ref:`DocumentVersionV2`.


.. _DocumentVersionV2:

DocumentVersionV2
-----------------

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
- ``SupportsContentPatching``— флаг, указывающий, что тип поддерживает :doc:`подготовку к подписанию <../instructions/preparetosign>` документа.
- ``SupportsEncrypting`` — флаг, указывающий, что тип поддерживает отправку зашифрованных документов.
- ``SupportsPredefinedRecipientTitle``— флаг, указывающий, что тип поддерживает отправкуа :doc:`предопределенного титула получателя <../howto/example_predefined_recipient_title>`.
- ``SupportsAmendmentRequest``— флаг, указывающий, что тип поддерживает отправку запрос на уточнение.
- ``Titles`` — список титулов документов. Каждый титул представлен структурой :ref:`DocumentTitleV2`.
- ``IsActual`` — флаг, указывающий, что версия документа актуальна.
- ``Workflows`` — список видов документооборота для текущего типа. Каждый вид представлен структурой :doc:`DocumentWorkflow`.


.. _DocumentTitleV2:

DocumentTitleV2
---------------

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
- ``UserDataXsdUrl`` — URL-путь метода, возвращающего XSD-схему ``UserDataXsd`` для генерации титула с помощью метода :doc:`../http/GenerateTitleXml`. Если отсутствует, то генерация титула под этим индексом не реализована.
- ``SignerInfo`` — информация о подписанте титула, представленная структурой :ref:`SignerInfoV2`.
- ``MetadataItems`` — метаданные документа, представленные структурой :ref:`DocumentMetadataItemV2`.
- ``EncryptedMetadataItems`` — метаданные зашифрованного документа, представленные структурой :ref:`DocumentMetadataItemV2`.


.. _SignerInfoV2:

SignerInfoV2
------------

Структура ``SignerInfoV2`` представляет собой информацию о подписанте титула.

.. code-block:: protobuf

    message SignerInfoV2 {
        required int32 SignerType = 1;
        required int32 ExtendedDocumentTitleType = 2 [default = -1];
        optional string SignerUserDataXsdUrl = 3;
    }

- ``SignerType`` — тип подписанта титула. Принимает одно из следующих значений:

	- 0 — подписант отсутствует, формируется только файл открепленной подписи. Используется для неформализованных документов.
	- 1 — простой подписант. Используется для документов форматов :doc:`@93/@172 <../docflows/AttachmentVersion>` и своих типов документов не на базе форматов :doc:`@155/@820 <../docflows/AttachmentVersion>`.
	- 2 — расширенный подписант. Используется для документов форматов :doc:`@155/@189/@551/@552/@736/@820 <../docflows/AttachmentVersion>` и своих типов документов на базе форматов :doc:`@155/@820 <../docflows/AttachmentVersion>`.
	- 3 — универсальный подписант. Используется, если заполнено поле ``SignerUserDataXsdUrl``.

- ``ExtendedDocumentTitleType`` — тип титула документа, для которого нужно заполнить дополнительные данные о подписанте. Принимает одно из следующих значений:

	- -1 — указывается для типов подписанта 0, 1 или 3,
	- 0 — данные для титула продавца УПД,
	- 1 — данные для титула покупателя УПД,
	- 2 — данные для титула продавца УКД,
	- 3 — данные для титула покупателя УКД,
	- 4 — данные для титула продавца формата 551,
	- 5 — данные для титула покупателя формата 551,
	- 6 — данные для титула исполнителя формата 552,
	- 7 — данные для титула для титула заказчика формата 552,
	- 8 — данные для титула покупателя УПД формата 820,
	- 9 — данные для титула покупателя Торг-2,
	- 10 - данные для титула продавца Торг-2,
	- 11 — данные для титула покупателя УКД формата 736,
	- 12 — данные для титула продавца УПД формата 970,
	- 13 — данные для титула покупателя УПД формата 970.

- ``SignerUserDataXsdUrl`` — URL-путь метода, возвращающего файл XSD-схемы упрощенного XML подписанта.


.. _DocumentMetadataItemV2:

DocumentMetadataItemV2
----------------------

Структура ``DocumentMetadataItemV2`` представляет собой метаданные документа.

.. code-block:: protobuf

    message DocumentMetadataItemV2 {
        required string Id = 1;
        required int32 Type = 2;
        required bool IsRequired = 3;
        required int32 Source = 4;
    }

- ``Id`` — идентификатор метаданных.
- ``Type`` — тип значения метаданных. Принимает одно из следующих значений:

	- 0 — строка,
	- 1 — целое число,
	- 2 — число с десятичной точкой,
	- 3 — дата в формате ДД.ММ.ГГГГ,
	- 4 — время в формате чч:мм.

- ``IsRequired`` — флаг, указывающий на обязательность заполнения поля метаданных.
- ``Source`` — источник метаданных. Принимает одно из следующих значений:

	- 0 — метаданные содержатся в теле документа;
	- 1 — метаданные передаются в метод API отдельными полями.


----

.. rubric:: См. также

*Структура используется:*
	- в теле ответа метода :doc:`../http/GetDocumentTypes`