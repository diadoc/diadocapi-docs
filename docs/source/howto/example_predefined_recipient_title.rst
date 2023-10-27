Как работать с предопределённым титулом получателя
==================================================

Классическая схема обмена двухтитульными документами выглядит так:
отправитель готовит титул (отправителя, продавца, первый), подписывает его и отправляет вместе с подписью получателю.

В свою очередь, получатель готовит ответный титул (получателя, покупателя, второй), и также подписывает и отправляет его вместе с подписью.


Схема через предопределённый титул позволяет отправителю приложить сразу оба титула. Получателю останется лишь проверить его валидность и подписать, либо же отказать в подписи.

Примеры использования (C#)
--------------------------
Узнать версию типа, которая поддерживает такую отправку, можно через метод :doc:`../http/GetDocumentTypes` (поле SupportsPredefinedRecipientTitle = true).

Сейчас отправить документ с двумя титулами сразу можно через шаблоны:

.. code-block:: csharp

  var senderTitle = File.ReadAllBytes("C:\\path\\to\\sender\\title.xml");
  var recipientTitle = File.ReadAllBytes  ("C:\\path\\to\\recipient\\title.xml");

  var documentAttachmentWithTwoTitles = new TemplateDocumentAttachment
    {
      // Указать тип, для версии которого разрешен предопределённый титул покупателя
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


Далее получатель превращает шаблон в документ:

.. code-block:: csharp

  var templateDocumentToTransform = template
      .Entities
      .FirstOrDefault(e => e.DocumentInfo.TypeNamedId == "typenamedid");

  var transformationToPost = new TemplateTransformationToPost
    {
      BoxId = toBoxId,
      TemplateId = template.MessageId,
      DocumentTransformations =
      {
        new DocumentTransformation
          {
            DocumentId = templateDocumentToTransform.EntityId
          }
      }
    };

    api.TransformTemplateToMessage(authToken, transformationToPost);

После превращения документу требуется подпись, чтобы дойти до получателя.
Отправитель документа `(messageFromBoxId)` генерирует подпись и отправляет к своему титулу:

.. code-block:: csharp

			var senderTitleContent = message
				.Entities
				.FirstOrDefault(e => e.EntityId == documentId)
				.Content;

			var signatureForSenderTitlePatch = new MessagePatchToPost
			{
				Signatures =
				{
					new DocumentSignature
					{
						ParentEntityId = documentId;
						Signature = crypt.Sign(senderTitleContent.Data, senderCertificateContent)
					}
				}
			}; 

Нужные entityId сущностей титулов отправителя и получателя можно получить через метод :doc:`../http/GetMessage`.


До получателя документа дойдет как подписанный титул отправителя, так и неподписанный предопределенный титул получателя. С его стороны останется также отправить подпись, но уже к предопределённому титулу:

.. code-block:: csharp

			var recipientTitleContent = message
				.Entities
				.FirstOrDefault(e => e.EntityId == recipientTitleEntityId)
				.Content;
			
			var signatureForRecipientTitlePatch = new MessagePatchToPost
			{
				Signatures =
				{
					new DocumentSignature
					{
						ParentEntityId = documentId;
						Signature = crypt.Sign(recipientTitleContent.Data, recipientCertificateContent)
					}
				}
			};

			api.PostMessagePatch(authToken, signatureForRecipientTitlePatch);


