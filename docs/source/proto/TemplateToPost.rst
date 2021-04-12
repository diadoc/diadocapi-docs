TemplateToPost
==============

Структура данных *TemplateToPost* представляет сообщение, подлежащее отправке через Диадок при помощи метода :doc:`../http/PostTemplate`.

.. code-block:: protobuf

    message TemplateToPost {
        required string FromBoxId = 1;
        required string ToBoxId = 2;
        required string MessageFromBoxId = 3;
        required string MessageToBoxId = 4;
        optional string MessageToDepartmentId = 5;
        repeated TemplateDocumentAttachment DocumentAttachments = 6;
        optional LockMode LockMode = 7 [default = None];
        optional string FromDepartmentId = 8;     
        optional string ToDepartmentId = 9;
        optional string MessageProxyBoxId = 10;
        optional string MessageProxyDepartmentId = 11;
        optional bool IsReusable = 12 [default = false];
    }


- *FromBoxId* - идентификатор ящика отправителя сообщения.

- *ToBoxId* - идентификатор ящика получателя сообщения. Должен отличаться от идентификатора ящика отправителя. Для внутреннего документа (IsInternal = true) этот идентификатор должен оставаться пустым (отсутствовать или содержать пустую строку).

- *MessageFromBoxId* - идентификатор ящика отправителя документов, созданных на основе шаблонов.

- *MessageToBoxId* - идентификатор ящика получателя документов, созданных на основе шаблонов.

- *MessageToDepartmentId* - идентификатор подразделения получателя сообщения, которое будет создано на основе отправляемого шаблона.

- *DocumentAttachments* - список документов любых типов, содержащий сообщение :doc:`../proto/TemplateDocumentAttachment`.

- *LockMode* - режим блокировки сообщения с шаблонами. Виды доступных режимы доступны в описании :doc:`../proto/LockMode`.

- *FromDepartmentId* - идентификатор подразделения отправителя сообщения.

- *ToDepartmentId* - идентификатор подразделения в организации получателя, в которое будут отправлены все шаблоны из сообщения (может отсутствовать, в этом случае шаблоны будут отправлены в головное подразделение).

- *MessageProxyBoxId* - идентификатор ящика промежуточного получателя документов, созданных на основе шаблонов.

- *MessageProxyDepartmentId* - идентификатор подразделения промежуточного получателя сообщения, которое будет создано на основе отправляемого шаблона.

- *IsReusable* - флаг, устанавливающий, можно ли использовать шаблон больше одного раза.

Сохраненный таким образом шаблон можно будет найти используя метод :doc:`../http/GetMessage`.
