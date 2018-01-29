TemplateToPost
==============

Структура данных *TemplateToPost* представляет сообщение, подлежащее отправке через Диадок при помощи метода :doc:`../http/PostTemplate`.

.. code-block:: protobuf

    message TemplateToPost {
        required string FromBoxId = 1;
        required string ToBoxId = 2;
        required string MessageFromBoxId = 3;
        required string MessageToBoxId = 4;
        optional string DocumentRecipientDepartmentId = 5;
        repeated TemplateDocumentAttachment DocumentAttachments = 6;
    }


    :param FromBoxId: идентификатор ящика отправителя сообщения.

    :param ToBoxId: идентификатор ящика получателя сообщения. Должен отличаться от идентификатора ящика отправителя. Для внутреннего документа (IsInternal = true) этот идентификатор должен оставаться пустым (отсутствовать или содержать пустую строку).

    :param MessageFromBoxId: идентификатор ящика отправителя документов, созданных на основе шаблонов.

    :param MessageToBoxId: идентификатор ящика получателя документов, созданных на основе шаблонов.

    :param DocumentRecipientDepartmentId: идентификатор подразделения отправителя сообщения, которое будет создано на основе отправляемого шаблона.

    :param DocumentAttachments: список документов любых типов, содержащий сообщение :doc:`../proto/TemplateDocumentAttachment`.

Сохраненный таким образом шаблон можно будет найти используя метод :doc:`../http/GetTemplate`.