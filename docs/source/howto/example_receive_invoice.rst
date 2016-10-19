Как получить счет-фактуру
=========================

Рассмотрим последовательность действий к функциям интеграторского интерфейса Диадока, которые требуется совершить покупателю при получении счета-фактуры (СФ), корректировочного счета-фактуры (КСФ), исправления счета-фактуры (ИСФ).

#. Продавец отправляет счет-фактуру Покупателю.

#. Диадок должен сформировать подтверждение оператора о дате отправки счета-фактуры, подписать его и направить Покупателю.

#. Покупатель получает счет-фактуру и подтверждение оператора и отправляет в ответ подписанные извещение о получении счета-фактуры и извещение о получении подтверждения.

#. Диадок формирует подтверждение оператора о дате отправки извещения о получении счета-фактуры, подписывает его и направляет Покупателю.

#. Покупатель получает подтверждение оператора и отправляет в ответ подписанное извещение о получении подтверждения.


.. note:: Более подробно о порядке обмена электронными счетами-фактурами между компаниями можно почитать в :doc:`соответствующем разделе <../InvoiceDocflow>` или на `сайте <http://www.diadoc.ru/docs/e-invoice/interchange>`__

Поиск счета-фактуры
-------------------

Сначала необходимо найти входящие счета-фактуры, которые требуется обработать, для этого нужно воспользоваться методом :doc:`../http/GetDocuments`:

  -  в значение параметра *boxId* указываем идентификатор ящика, в котором следует выполнить поиск входящих документов,

  -  параметр *filterCategory* задается в виде строки, в данном примере ``AnyInvoiceDocumentType.InboundNotFinished``

Пример запроса на получение счета-фактуры выглядит следующим образом:

::

    GET /V3/GetDocuments?filterCategory=AnyInvoiceDocumentType.InboundNotFinished&boxId=db32772b-9256-49a8-a133-fda593fda38a HTTP/1.1
    Host: diadoc-api.kontur.ru
    Accept: application/json
    Content-Type: application/json charset=utf-8
    Authorization: DiadocAuth ddauth_api_client_id=testClient-87e1638deae84c86b8e2069955c2825a0987

В теле ответа вернется список документов в виде структуры *DocumentList* с вложенной структурой *Document*. Для каждого из этих документов запоминаем: *MessageId*, *EntityId*.

.. code-block:: json

   {
      "TotalCount": 1,
      "Documents": [
        {
          "IndexKey": "2B7732DB5692A849A133FDA593FDA38A9279A2CBA18EDF49B3D5CAE8D97C89B0ED4D67F0183510448F64919BE6B8F35B0000000000000000000000000000000000104608D2D2D8BA8731D80DDBCEBB34CE0D4EB3213F600C920935072CCF309772484DBC6FCA7A80E2CF95",
          "MessageId": "bbcedb0d-ce34-4e0d-b321-3f600c920935",
          "EntityId": "30cf2c07-7297-4d48-bc6f-ca7a80e2cf95",
          "CreationTimestampTicks": 635802325536912186,
          "CounteragentBoxId": "95f642cd1256426fb11c883c73d8440a@diadoc.ru",
          "DocumentType": "Invoice",
          "InitialDocumentIds": [],
          "SubordinateDocumentIds": [],
          "Content": "lores ipsum",
          "FileName": "ON_SFAKT_2BM-7770357771-2012082810454029703720000000000_2BM-7750370234-4012052808304878702630000000000_20150826_d37c6a05-e85c-4469-8c68-2d0303f61c2a.xml",
          "DocumentDate": "26.08.2015",
          "DocumentNumber": "432634",
          "InvoiceMetadata":
            {
              "InvoiceStatus": "InboundNotFinished",
              "Total": "17700.00",
              "Vat": "2700.00",
              "Currency": 643,
              "ConfirmationDateTimeTicks": 635802433696852440,
              "InvoiceAmendmentFlags": 0
            },
          "IsDeleted": false,
          "DepartmentId": "00000000-0000-0000-0000-000000000000",
          "IsTest": true,
          "FromDepartmentId": "00000000-0000-0000-0000-000000000000",
          "ToDepartmentId": "",
          "CustomDocumentId": "",
          "RevocationStatus": "RevocationStatusNone",
          "SendTimestampTicks": 635802325536912186,
          "DeliveryTimestampTicks": 635802325696852440,
          "ForwardDocumentEvents": [],
          "RoamingNotificationStatus": "RoamingNotificationStatusNone",
          "HasCustomPrintForm": false,
          "CustomData": [],
          "DocumentDirection": "Inbound",
          "LastModificationTimestampTicks": 635802325696852440,
          "IsEncryptedContent": false,
          "SenderSignatureStatus": "SenderSignatureCheckedAndValid",
          "MessageIdGuid": "bbcedb0d-ce34-4e0d-b321-3f600c920935",
          "EntityIdGuid": "30cf2c07-7297-4d48-bc6f-ca7a80e2cf95",
          "CreationTimestamp": "2015-10-12T07:42:33.6912186Z",
          "CounteragentBoxIdGuid": "95f642cd-1256-426f-b11c-883c73d8440a"
        }]
    }

.. _receive_confirmation:

Получение счета-фактуры и подтверждения оператора
-------------------------------------------------

Затем необходимо получить найденный СФ :doc:`Invoice <../proto/Entity message>` и подтверждение оператора :doc:`InvoiceConfirmation <../proto/Entity message>`.

Подтверждение оператора представляется структурой :doc:`Entity <../proto/Entity message>`, где значение полей ``EntityType`` и ``AttachmentType`` должно быть *Attachment/InvoiceConfirmation*, СФ представляется структурой *Attachment/Invoice*.

Чтобы получить СФ и подтверждение оператора нужно вызвать метод :doc:`../http/GetMessage` и указать нужные GET-параметры ``boxId``, ``messageId``, ``entityId``.

``BoxId`` - это идентификатор ящика получателя, ``messageId`` - идентификатор полученного сообщения с СФ/ИСФ/КСФ/ИКСФ, ``entityId`` - идентификатор счета-фактуры. Их можно взять из структуры :doc:`../proto/Message`

::

    GET /V3/GetMessage?messageId=bbcedb0d-ce34-4e0d-b321-3f600c920935&entityId=30cf2c07-7297-4d48-bc6f-ca7a80e2cf95&boxId=db32772b-9256-49a8-a133-fda593fda38a HTTP/1.1
    Host: diadoc-api.kontur.ru
    Accept: application/json
    Content-Type: application/json charset=utf-8
    Authorization: DiadocAuth ddauth_api_client_id=testClient-87e1638deae84c86b8e2069955c2825a0987

Пример структуры подтверждения оператора :doc:`InvoiceConfirmation <../proto/Entity message>` в теле ответа:

.. code-block:: json

   {
       "EntityType": "Attachment",
       "EntityId": "654ac483-0dd4-4085-b70f-565c8b754e10",
       "ParentEntityId": "30cf2c07-7297-4d48-bc6f-ca7a80e2cf95",
       "Content": "lores ipsum",
       "AttachmentType": "InvoiceConfirmation",
       "FileName": "DP_PDPOL_2BM-7750370234-4012052808304878702630000000000_2BM_20150927_324c290e-f049-4906-baac-1ddcd7f3c2ff.xml",
       "NeedRecipientSignature": false,
       "SignerBoxId": "",
       "NotDeliveredEventId": "",
       "RawCreationDate": 635789700936777240,
       "SignerDepartmentId": "",
       "NeedReceipt": false,
       "IsApprovementSignature": false,
       "IsEncryptedContent": false
   }

.. _create_invoice_receipt:

Формирование извещения о получении подтверждения оператора
----------------------------------------------------------

После того, как покупатель получил подтверждение оператора, он должен отправить в ответ подписанное извещение :doc:`InvoiceReceipt  <../proto/Entity message>` о получении подтверждения.

Извещение о получении подтверждения оператора представляется структурой :doc:`Entity <../proto/Entity message>`, где значение полей ``EntityType`` и ``AttachmentType`` должно быть *Attachment/InvoiceReceipt*.

В API Диадока есть метод, который позволяет сформировать извещение о получении подтверждения оператора - :doc:`../http/GenerateInvoiceDocumentReceiptXml`, при вызове этого метода нужно корректно указать GET-параметры ``boxId``, ``messageId``, ``attachmentId`` и передать в тело запроса данные о подписанте генерируемого извещения в виде сериализованной структуры :doc:`../proto/Signer`.

``BoxId`` - это идентификатор ящика отправителя, ``messageId`` - идентификатор отправленного сообщения с СФ/ИСФ/КСФ/ИКСФ, ``attachmentId`` - идентификатор подтверждение оператора. Их можно взять из структуры :doc:`../proto/Message`.

Например HTTP-запрос для формирования извещение о получении подтверждения оператора выглядит следующим образом:

::

    POST /GenerateInvoiceDocumentReceiptXml?boxId=db32772b-9256-49a8-a133-fda593fda38a&messageId=a9093c56-7c48-4ab1-bc87-efb04e7d4400&attachmentId=f80738a3-b0bc-426a-aadf-6967ec1b53df HTTP/1.1
    Host: diadoc-api.kontur.ru
    Content-Type: application/json charset=utf-8
    Accept: application/json
    Authorization: DiadocAuth ddauth_api_client_id=testClient-87e1638deae84c86b8e2069955c2825a0987

Пример структуры в теле запроса, содержащей данные о подписанте генерируемого извещения :doc:`../proto/Signer`:

.. code-block:: json

   {
       "SignerCertificate": "",
       "SignerDetails ": {
        "Surname": "Иванов",
        "FirstName": "Иван",
        "Patronymic": "Иванович",
        "JobTitle": "QA",
        "Inn": "1234567",
        "SoleProprietorRegistrationCertificate": "",
       },
   }

В теле ответа содержится XML-файл с извещением о получении документа ``attachmentId`` из сообщения ``messageId`` в ящике ``boxId``.

.. _send_receipt:

Отправка извещения о получении подтверждения оператора
------------------------------------------------------

Полученное на предыдущем этапе извещение нужно подписать и отправить. Подписание извещения происходит на стороне клиента, после того как извещение подписано, его нужно отправить вместе с файлом подписи воспользовавшись методом :doc:`../http/PostMessagePatch`.

Для этого нужно подготовить структуру :doc:`../proto/MessagePatchToPost` следующим образом:

-  в значение атрибута *BoxId* указываем идентификатор ящика получателя,

-  в значение атрибута *MessageId* указываем идентификатор модифицируемого сообщения,

-  для передачи XML-файла извещения нужно использовать атрибут *Receipts*, описываемый структурой *ReceiptAttachment*
  
  -  в поле *ParentEntityId* нужно указать идентификатор (*EntityId*) подтверждения оператора, полученный на предыдущем шаге,

  -  внутри структуры *ReceiptAttachment* находится вложенная структура *SignedContent*,
  
  -  сам XML-файл нужно передать в атрибут *Content*, подпись продавца в атрибут *Signature*

.. code-block:: protobuf

    message MessagePatchToPost {
        required string BoxId = 1;
        required string MessageId = 2;
        repeated ReceiptAttachment Receipts = 3;
    }

    message ReceiptAttachment  {
        required string ParentEntityId  = 1;
        required SignedContent SignedContent = 2;

    }

    message SignedContent {
        optional bytes Content = 1;
        optional bytes Signature = 2;
    }

Пример структуры в теле запроса, содержащей данные о передаваемом извщении :doc:`../proto/MessagePatchToPost`:

.. code-block:: json

    {
      "BoxId": "db32772b-9256-49a8-a133-fda593fda38a",
      "MessageId": "a9093c56-7c48-4ab1-bc87-efb04e7d4400",
      "Receipts":
      [
        {
          "ParentEntityId":"f80738a3-b0bc-426a-aadf-6967ec1b53df",
          "SignedContent":
            {
              "Content": "...",
              "Signature": "...",
            },
          "Comment": "Подписание извщения о получении подтверждения оператора",
        }
     ]
    }

Формирование извещения о получении счета-фактуры
------------------------------------------------

Также покупатель должен отправить в ответ подписанное извещение :doc:`InvoiceReceipt  <../proto/Entity message>` о получении СФ.

Извещение о получении СФ представляется структурой :doc:`Entity <../proto/Entity message>` как и извещение о получении подтверждения оператора.

Последовательность действий для формирования извещения о получении СФ аналогична последовательности действий для формирования извещения о получении подтверждения оператора (см. :ref:`create_receipt`).

За исключением того, что в ``attachmentId`` нужно указать идентификатор полученного счета-фактуры.

Отправка извещения о получении счета-фактуры
--------------------------------------------

Последовательность действий для отправки сформированного извещения о получении СФ аналогична последовательности действий для отправки сформированного извещения о получении подтверждения оператора.

За исключением того, что в в поле *ParentEntityId* нужно указать идентификатор (*EntityId*) СФ, полученного на предыдущем шаге (см. :ref:`send_receipt`).

Подтверждения оператора о дате отправки извещения о получении счета-фактуры
---------------------------------------------------------------------------

После того, как покупатель сформировал и отправил извещение о дате получении СФ, оператор в ответ должен сформировать подтверждение оператора о дате отправки извещения о получении СФ.

Это подтверждение покупатель должен получить, затем сформировать извещение о получении подтверждения оператора, подписать его и отправить.

Получение подтверждения оператора описано в разделе :ref:`receive_confirmation`.

Формирование извещения о получении подтверждения оператора описано в разделе :ref:`create_receipt`.

Подписание и отправка извещения описаны разделе :ref:`send_receipt`.

После того, как покупатель сформировал все необходимые извещения, счет-фактура перейдет в статус *InboundFinished*

Запрос уточнения/корректировки по счету-фактуре
-----------------------------------------------

Для того чтобы создать запрос на уточнение или корректировку счета-фактуры, необходимо сформировать через API xml-уведомление об уточнении/корректировке с помощью метода :doc:`../http/GenerateInvoiceCorrectionRequestXml`.

После того, как будет получен XML-файл, его нужно отправить с помощью команды :doc:`../http/PostMessagePatch`

Для этого нужно подготовить структуру :doc:`../proto/MessageToPost` следующим образом:

-  Структура данных *CorrectionRequestAttachment* представляет одно уведомление об уточнении СФ/ИСФ/КСФ/ИКСФ в отправляемом патче,
 
-  *ParentEntityId* - идентификатор СФ/ИСФ/КСФ/ИКСФ, к которому относится данное уведомление. Это идентификатор соответствующей сущности из родительского сообщения (поле *EntityId* в структуре :doc:`Entity <../proto/Entity message>`).
 
-  *SignedContent* - содержимое файла уведомления вместе с ЭЦП под ним в виде структуры SignedContent.

SDK
---

Пример кода на C# для получения счета фактуры:

.. code-block:: csharp

	//Для работы с документами в Диадоке необходим авторизационный токен.
	//Подробнее о получении авторизационного токена можно узнать в разделе "Как авторизоваться в системе".
	public static string AuthTokenCert;
	
	public static string BoxId = "идентификатор ящика получателя";

	//Для работы с документом необходимо знать его уникальный идентификатор.
	//Узнать идентификатор можно, например, выполнив поиск документов по заданным параметрам.

	//Получение списка всех счетов-фактур, по которым не завершен документооборот
	public static DocumentList SearchInboundInvoicesDocumentsWithNotFinishedDocflow()
	{
		//Параметры, по которым осуществляется фильтрация
		var filterCategory = "Invoice.InboundNotFinished";
		var counteragentBoxId = "идентификатор ящика отправителя";

		return Api.GetDocuments(AuthTokenCert, BoxId, filterCategory, counteragentBoxId);
	}
		
	//Получение сообщения, содержащего счет-фактуру 
	public static Message GetInvoice()
	{
		//Выбираем конкретный документ из полученного ранее списка.
		//Например, самый первый.
		var document = SearchInboundInvoicesDocumentsWithNotFinishedDocflow().Documents[0];

		//Получение счета-фактуры
		return Api.GetMessage(AuthTokenCert, BoxId, document.MessageId, document.EntityId);
	}
	
	//Получение подтверждения оператора, формирование и отправка извещения о получении подтверждения
	public static void GetInvoiceConfirmationAndSendInvoiceReceipt(Message invoiceMessage)
	{
		//Выбор первого вложения типа InvoiceConfirmation, к которому нет извещения о получении
		var confirmationEntities = invoiceMessage.Entities
			.FindAll(entity => entity.AttachmentType == AttachmentType.InvoiceConfirmation);
		var receiptEntitiesParentIds = invoiceMessage.Entities
			.FindAll(entity => entity.AttachmentType == AttachmentType.InvoiceReceipt)
			.Select(receiptEntity => receiptEntity.ParentEntityId);
		var confirmationEntityWithoutReceiptId = confirmationEntities
			.First(confirmationEntity => !receiptEntitiesParentIds
				.Contains(confirmationEntity.EntityId)).EntityId;
		
		var receipt = Api.GenerateInvoiceDocumentReceiptXml(AuthTokenCert, BoxId, invoiceMessage.MessageId, confirmationEntityId, new Signer()
		{
			//Подпись получателя, см. "Как авторизоваться в системе"
			SignerCertificate = ReadCertContent("путь к сертификату"),
			SignerDetails = new SignerDetails()
			{
				//Заполняется согласно структуре SignerDetails
			}
		});
		
		var receiptAttachment = new ReceiptAttachment()
		{
			ParentEntityId = confirmationEntityId,
			SignedContent = new SignedContent()
			{
				Content = receipt.Content,
				//Подпись получателя, см. "Как авторизоваться в системе"
				Signature = Crypt.Sign(receipt.Content, ReadCertContent("путь к сертификату"))
			}
		};
		
		var receiptPatch = new MessagePatchToPost()
		{
			BoxId = BoxId,
			MessageId = invoiceMessage.MessageId,
			Receipts =
			{
				receiptAttachment
			}
		};

		Api.PostMessagePatch(AuthTokenCert, receiptPatch);
	}
	
	//Формирование и отправка извещения о получении счета-фактуры
	public static void SendinvoiceReceipt(Document invoiceDocument)
	{
		var receipt = Api.GenerateInvoiceDocumentReceiptXml(AuthTokenCert, BoxId, invoiceDocument.MessageId, invoiceDocument.EntityId, new Signer()
		{
			//Подпись получателя, см. "Как авторизоваться в системе"
			SignerCertificate = ReadCertContent("путь к сертификату"),
			SignerDetails = new SignerDetails()
			{
				//Заполняется согласно структуре SignerDetails
			}
		});
		
		var receiptAttachment = new ReceiptAttachment()
		{
			ParentEntityId = invoiceDocument.EntityId,
			SignedContent = new SignedContent()
			{
				Content = receipt.Content,
				//Подпись получателя, см. "Как авторизоваться в системе"
				Signature = Crypt.Sign(receipt.Content, ReadCertContent("путь к сертификату"))
			}
		};
		
		var receiptPatch = new MessagePatchToPost()
		{
			BoxId = BoxId,
			MessageId = invoiceDocument.MessageId,
			Receipts =
			{
				receiptAttachment
			}
		};

		Api.PostMessagePatch(AuthTokenCert, receiptPatch);
	}
	
	public static void Main()
	{
		var invoiceMessage = GetInvoice();
		var invoiceDocument = invoiceMessage.Entities.First(entity => entity.AttachmentType == AttachmentType.Invoice);
		
		//Отправка извещения о получении подтверждения оператора для счета-фактуры
		GetInvoiceConfirmationAndSendInvoiceReceipt(invoiceMessage);
		
		//Отправка извещения о получении счета-фактуры
		SendinvoiceReceipt(invoiceDocument);
		
		//Отправка извещения о получении подтверждения оператора для извещения о получении счета-фактуры
		GetInvoiceConfirmationAndSendInvoiceReceipt(invoiceMessage);
	}

Пример кода на C# для отправки уведомления об уточнении счета-фактуры:

.. code-block:: csharp

	//формирование уведомления об уточнении счета-фактуры
	public static GeneratedFile GetInvoiceCorrectionRequest(Document invoiceDocument)
	{
		var invoiceCorrectionRequestInfo = new InvoiceCorrectionRequestInfo()
		{
			ErrorMessage = "Текст уведомления об уточнении",
			Signer = new Signer()
			{
				//Подпись отправителя, см. "Как авторизоваться в системе"
				SignerCertificate = ReadCertContent("путь к сертификату"),
				SignerDetails = new SignerDetails()
				{
					//Заполняется согласно структуре SignerDetails
				}
			}
		};
		return Api.GenerateInvoiceCorrectionRequestXml(AuthTokenCert, BoxId, invoiceDocument.MessageId, invoiceDocument.EntityId, invoiceCorrectionRequestInfo);
	}
	
	//Отправка уведомления об уточнении счета-фактуры
	public static void SendInvoiceCorrectionRequest(Document invoiceDocument)
	{
		var invoiceCorrectionRequest = GetInvoiceCorrectionRequest(invoiceDocument);

		var messagePatchToPost = new MessagePatchToPost
		{
			MessageId = invoiceDocument.MessageId,
			CorrectionRequests =
			{
				new CorrectionRequestAttachment
				{
					ParentEntityId = invoiceDocument.EntityId,
					SignedContent = new SignedContent //файл подписи
					{
						Content = invoiceCorrectionRequest.Content,
						//Подпись получателя, см. "Как авторизоваться в системе"
						Signature = Crypt.Sign(invoiceCorrectionRequest.Content, ReadCertContent("путь к сертификату"))
					}
				}
			}
		};
		Api.PostMessagePatch(AuthTokenCert, messagePatchToPost);
	}
	
	public static void Main()
	{
		var invoiceDocument = GetInvoice().Entities.First(entity => entity.AttachmentType == AttachmentType.Invoice);;
		SendInvoiceCorrectionRequest(invoiceDocument);
	}