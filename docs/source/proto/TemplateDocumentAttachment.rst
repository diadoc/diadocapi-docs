TemplateDocumentAttachment
==========================

Представляет в отправляемом сообщении :doc:`TemplateToPost` документ любого типа.

.. code-block:: protobuf

    message TemplateDocumentAttachment {
        required UnsignedContent UnsignedContent = 1;
        optional string Comment = 2;
        required string TypeNamedId = 3;
        optional string Function = 4;
        optional string Version = 5;
        repeated MetadataItem Metadata = 6;
        optional int32 WorkflowId = 7;
        optional string CustomDocumentId = 8;
        optional string EditingSettingId = 9;
        optional bool NeedRecipientSignature = 10 [default = false];
        optional PredefinedRecipientTitle PredefinedRecipientTitle = 11;
        optional bool RefusalDisabled = 12 [default = false];
        repeated CustomDataItem CustomData = 13;
    }

    message PredefinedRecipientTitle {
        required UnsignedContent UnsignedContent = 1;
    }

- *UnsignedContent* - содержимое файла в виде структуры :doc:`UnsignedContent`.

- *Comment* - необязательный текстовый комментарий к документу. Максимально допустимая длина - 5000 символов.

- *TypeNamedId* - строковой идентификатор типа документа. Доступные типы можно получить методом :doc:`../http/GetDocumentTypes`.

- *Function* - идентификатор функции документа. Обязательно при отправке зашифрованных документов.

- *Version* - идентификатор версии документа. Обязательно при отправке зашифрованных документов.

- *Metadata* - список пар вида "ключ-значение", содержащих метаданные документа. Каждая пара задается структурой :doc:`MetadataItem`. Список доступных метаданных для типа можно получить через метод :doc:`../http/GetDocumentTypes`.

- *WorkflowId* - идентификатор вида документооборота. Список допустимых видов документооборота для типа можно получить через метод :doc:`../http/GetDocumentTypes`. Описание видов документооборота доступно на странице :doc:`DocumentWorkflow`.

- *CustomDocumentId* - необязательный идентификатор документа во внешней системе, уникальный в рамках структуры :doc:`TemplateToPost`; используется для выстраивания связей между документами внутри отправляемого сообщения. В дальнейшем его можно получить через *Document.CustomDocumentId*.

- *EditingSettingId* - идентификатор настройки редактирования содержимого документа. Наличие данной настройки означает, что в содержимом файла может отсутствовать контент, редактирование которого разрешено данной настройкой.

- *NeedRecipientSignature* - необязательный признак, обозначающий запрос подписи получателя под отправляемым документом, созданным из шаблона. При его проставлении документ, который будет создан из шаблона, будет требовать подпись от получателя.

- *PredefinedRecipientTitle* - необязательное поле для данных о титуле получателя. Предназначено для двухтитульных документов с разрешённой для действия версией. Подробнее о функционале можно узнать здесь: :doc:`../howto/example_predefined_recipient_title`.

- *RefusalDisabled* - необязательный признак, управляющий возможностью отклонять шаблон на стороне получателя. Если выставить при знак в true, то у получателя шаблона не будет возможности отклонить его.

- *CustomData* - список пар вида "ключ-значение", содержащих произвольные данные по документу. Каждая пара задается структурой :doc:`CustomDataItem`.
