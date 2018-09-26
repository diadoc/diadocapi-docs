Как работать с предопределённым титулом покупателя
==================================================


Классическая схема обмена двухтитульными документами выглядит так:
отправитель готовит титул (титул отправителя, титул продавца, первый титул), подписывает его и отправляет вместе с подписью получателю.
В свою очередь, получатель готовит ответный (титул получателя, покупателя, второй), и также подписывает и отправляет его вместе с подписью.


Схема через предопределённый титул позволяет отправителю приложить сразу оба титула. Покупателю останется лишь проверить его валидность и подписать, либо же отказать в подписи.

Примеры использования (C#)
--------------------------

- Создание

Сейчас отправить документ с двумя титулами сразу можно лишь через шаблоны:

.. code-block:: csharp

  var senderTitle = File.ReadAllBytes("C:\\path\\to\\sender\\title.xml");
  var recipientTitle = File.ReadAllBytes  ("C:\\path\\to\\recipient\\title.xml");

  var documentAttachmentWithTwoTitles = new TemplateDocumentAttachment
    {
      // Указать тип, для версии которого разрешен предопределённый титул покупателя (SupportsPredefinedRecipientTitle = true)
      // Саму версию явно можно не указывать, т.к. она должна быть указана  под узлом ВерсФорм в XML.
      TypeNamedId = "typenamedid",
      UnsignedContent = new UnsignedContent
      {
        Content = senderTitle
      },
      PredefinedRecipientTitle = new PredefinedRecipientTitle
      {
        UnsignedContent = new UnsignedContent
        {
          Content = recipientTitle
        }
      }
    };

  var templateToPost = new TemplateToPost
    {
      FromBoxId = fromBoxId,
      ToBoxId = toBoxId,
      MessageFromBoxId = messageFromBoxId,
      MessageToBoxId = messageToBoxId,
      DocumentAttachments = {documentAttachmentWithTwoTitles}
    };

  var template = api.PostTemplate(authToken, templateToPost);

