Как отправить счет-фактуру
==========================

Рассмотрим последовательность действий к функциям интеграторского интерфейса Диадока, которые требуется совершить продавцу при отправке счета-фактуры (СФ), корректировочного счета-фактуры (КСФ), исправления счета-фактуры (ИСФ).

#. Продавец может сформировать счет-фактуру, подписать и направить Покупателю.

#. Диадок должен сформировать подтверждение оператора о дате получения счета-фактуры, подписать его и направить Продавцу.

#. Продавец должен получить подтверждение оператора и отправить в ответ подписанное извещение о получении подтверждения.


.. note:: Более подробно о порядке обмена электронными счетами-фактурами между компаниями можно почитать в :doc:`соответствующем разделе <../InvoiceDocflow>` или на `сайте <http://www.diadoc.ru/docs/e-invoice/interchange>`__

Формирование счета-фактуры
--------------------------

Если на стороне интеграционного решения не предусмотрено функциональности для формирования XML-документов, соответствующих утвержденным форматам, то продавец может сгенерировать СФ/ИСФ/КСФ/ИКСФ, используя команду :doc:`../http/GenerateInvoiceXml`.

Для формирования СФ/ИСФ/КСФ/ИКСФ в GET-параметр ``invoiceType`` нужно передать значение ``Invoice``.
	   
В теле запроса должны содержаться данные для изготовления СФ/ИСФ/КСФ/ИКСФ:
	
	-  в виде сериализованной структуры :doc:`../proto/InvoiceInfo` для типов документов ``Invoice`` или ``InvoiceRevision``
	
	-  в виде сериализованной структуры :doc:`../proto/InvoiceCorrectionInfo` для типов документов ``InvoiceCorrection`` или ``InvoiceCorrectionRevision``.
	   
Например, HTTP-запрос для генерации СФ выглядит следующим образом:

::

    POST /GenerateInvoiceXml?invoiceType=Invoice HTTP/1.1
    Host: diadoc-api.kontur.ru
    Authorization: DiadocAuth ddauth_api_client_id=testClient-8ee1638deae84c86b8e2069955c2825a
    Content-Length: 1252
    Connection: Keep-Alive

    <Сериализованная структура InvoiceInfo>

В теле ответа содержится XML-файл СФ/ИСФ/КСФ/ИКСФ, построенный на основании данных из запроса.

Успешный ответ сервера выглядит так:
::

    HTTP/1.1 200 OK
    Content-Length: 598

    <XML-файл СФ>

Файл СФ/ИСФ генерируется в соответствии с :download:`XML-схемой <../xsd/ON_SFAKT_1_897_01_05_02_01.xsd>`, которой должны удовлетворять XML-счета-фактуры, согласно приказу ФНС.

Файл КСФ/ИКСФ генерируется в соответствии с другой утвержденной ФНС :download:`XML-схемой <../xsd/ON_KORSFAKT_1_911_01_05_02_01.xsd>`. 

Имя файла СФ/ИСФ/КСФ/ИКСФ (формат которого также определяет приказ ФНС) возвращается в стандартном HTTP-заголовке ``Content-Disposition``.

Отправка счета-фактуры
----------------------

После того, как у вас есть XML-файл СФ/ИСФ/КСФ/ИКСФ, его нужно отправить с помощью команды :doc:`../http/PostMessage`. 

Для этого нужно подготовить структуру :doc:`../proto/MessageToPost` следующим образом:

-  в значение атрибута *FromBoxId* указываем идентификатор ящика отправителя,

-  в значение атрибута *ToBoxId* указываем идентификатор ящика получателя

-  для передачи XML-файла СФ/ИСФ/КСФ/ИКСФ нужно использовать атрибут *Invoices*, описываемый структурой *XmlDocumentAttachment*

	-  внутри структуры *XmlDocumentAttachment* находится вложенная структура *SignedContent*,
	
	-  сам XML-файл нужно передать в атрибут *Content*, подпись продавца в атрибут *Signature*
	   
Описание структур, используемых при отправке СФ/ИСФ/КСФ/ИКСФ:

.. code-block:: protobuf

    message MessageToPost {
        required string FromBoxId = 1;
        optional string ToBoxId = 2;
        repeated XmlDocumentAttachment Invoices = 3;
    }

    message XmlDocumentAttachment {
        required SignedContent SignedContent = 1;
        optional string Comment = 3;
    }

    message SignedContent {
        optional bytes Content = 1;
        optional bytes Signature = 2;
    }

После отправки в теле ответа будет содержаться отправленное сообщение, сериализованное в протобуфер :doc:`../proto/Message`.

Получение подтверждения
-----------------------

После успешной отправки СФ/ИСФ/КСФ/ИКСФ необходимо получить подтверждение оператора :doc:`InvoiceConfirmation <../proto/Entity message>`.

Подтверждение оператора представляется структурой :doc:`Entity <../proto/Entity message>`, где значение полей ``EntityType`` и ``AttachmentType`` должно быть *Attachment/InvoiceConfirmation*.

Чтобы получить подтверждение оператора нужно вызвать метод :doc:`../http/GetMessage` и указать нужные GET-параметры ``boxId``, ``messageId``, ``entityId``.

``BoxId`` - это идентификатор ящика отправителя, ``messageId`` - идентификатор отправленного сообщения с СФ/ИСФ/КСФ/ИКСФ, ``entityId`` - идентификатор счета-фактуры. Их можно взять из структуры :doc:`../proto/Message`

Например, HTTP-запрос для получения сообщения выглядит следующим образом:

::

    GET /V3/GetMessage?messageId=8971177a-8c38-49f7-97d3-0f51fbe134c5&entityId=736aa0c4-12f5-4412-bfea-1de59948b904&boxId=96339010-4c66-462d-a917-7f31bb8d80c4 HTTP/1.1
    Host: diadoc-api.kontur.ru
    Content-Type: application/json; charset=utf-8
    Accept: application/json
    Authorization: DiadocAuth ddauth_api_client_id=testClient-8ee1638deae84c86b8e2069955c2825a

Пример структуры подтверждения оператора :doc:`InvoiceConfirmation <../proto/Entity message>` в теле ответа:

.. code-block:: json

   {
       "EntityType": "Attachment",
       "EntityId": "9955dccd-82fd-4412-b953-7854e102f782",
       "ParentEntityId": "736aa0c4-12f5-4412-bfea-1de59948b904",
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

Формирование извещения о получении подтверждения оператора
----------------------------------------------------------

После того, как продавец получил подтверждение оператора, он должен отправить в ответ подписанное извещение :doc:`InvoiceReceipt  <../proto/Entity message>` о получении подтверждения.

Извещение о получении подтверждения оператора представляется структурой :doc:`Entity <../proto/Entity message>`, где значение полей ``EntityType`` и ``AttachmentType`` должно быть *Attachment/InvoiceReceipt*.

В API Диадока есть метод, который позволяет сформировать извещение о получении подтверждения оператора - :doc:`../http/GenerateInvoiceDocumentReceiptXml`, при вызове этого метода нужно корректно указать GET-параметры ``boxId``, ``messageId``, ``attachmentId`` и передать в тело запроса данные о подписанте генерируемого извещения в виде сериализованной структуры :doc:`../proto/Signer`.

``BoxId`` - это идентификатор ящика отправителя, ``messageId`` - идентификатор отправленного сообщения с СФ/ИСФ/КСФ/ИКСФ, ``attachmentId`` - идентификатор подтверждение оператора. Их можно взять из структуры :doc:`../proto/Message`.

Например, HTTP-запрос для формирования извещение о получении подтверждения оператора выглядит следующим образом:

::

    POST /GenerateInvoiceDocumentReceiptXml?boxId=db32772b-9256-49a8-a133-fda593fda38a&messageId=a9093c56-7c48-4ab1-bc87-efb04e7d4400&attachmentId=f80738a3-b0bc-426a-aadf-6967ec1b53df HTTP/1.1
    Host: diadoc-api.kontur.ru
    Content-Type: application/json charset=utf-8
    Accept: application/json
    Authorization: DiadocAuth ddauth_api_client_id=testClient-8ee1638deae84c86b8e2069955c2825a

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

Отправка извещения о получении подтверждения оператора
------------------------------------------------------

Полученное на предыдущем этапе извещение нужно подписать и отправить. Подписание извещения происходит на стороне клиента, после того как извещение подписано, его нужно отправить вместе с файлом подписи воспользовавшись методом :doc:`../http/PostMessagePatch`.

Для этого нужно подготовить структуру :doc:`../proto/MessagePatchToPost` следующим образом:

-  в значение атрибута *BoxId* указываем идентификатор ящика отправителя,

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

Пример структуры в теле запроса, содержащей данные о передаваемом извещении :doc:`../proto/MessagePatchToPost`:

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
          "Comment": "Подписание извещения о получении подтверждения оператора",
        }
     ]
    }

Получение извещения о получении счета-фактуры
---------------------------------------------

После того, как все действия со стороны продавца сделаны, нужно получить извещение о получении счета-фактуры со стороны покупателя :doc:`InvoiceReceipt <../proto/Entity message>`.

Извещение о получении счета-фактуры представляется структурой :doc:`Entity <../proto/Entity message>`, где значение полей ``EntityType`` и ``AttachmentType`` должно быть *Attachment/InvoiceReceipt*.

Чтобы получить подтверждение оператора нужно вызвать метод :doc:`../http/GetMessage` и указать нужные GET-параметры ``boxId``, ``messageId``, ``entityId``.

``BoxId`` - это идентификатор ящика отправителя, ``messageId`` - идентификатор отправленного сообщения с СФ/ИСФ/КСФ/ИКСФ, ``entityId`` - идентификатор счета-фактуры. Их можно взять из структуры :doc:`../proto/Message`

Например, HTTP-запрос для получения сообщения выглядит следующим образом:

::

    GET /V3/GetMessage?messageId=8971177a-8c38-49f7-97d3-0f51fbe134c5&entityId=736aa0c4-12f5-4412-bfea-1de59948b904&boxId=96339010-4c66-462d-a917-7f31bb8d80c4 HTTP/1.1
    Host: diadoc-api.kontur.ru
    Content-Type: application/json; charset=utf-8
    Accept: application/json
    Authorization: DiadocAuth ddauth_api_client_id=testClient-8ee1638deae84c86b8e2069955c2825a

Пример структуры извещения о получении счета-фактуры :doc:`InvoiceReceipt <../proto/Entity message>` в теле ответа:

.. code-block:: json

   {
       "EntityType": "Attachment",
       "EntityId": "1d7b2e96-9945-41ab-aeea-2f310382bfad",
       "ParentEntityId": "45d16c54-8700-4882-afaf-97678d6ed135",
       "Content": "lores ipsum",
       "AttachmentType": "InvoiceReceipt",
       "FileName": "DP_IZVPOL_2BM-9610384428-961001000-201510080625090688235_2BM-9653544919-965301000-201508270726013081470_20151008_6bbfab54-4e9f-4ca1-99eb-37f34880a784.xml",
       "NeedRecipientSignature": false,
       "SignerBoxId": "",
       "NotDeliveredEventId": "",
       "RawCreationDate": 635798950114653648,
       "SignerDepartmentId": "",
       "NeedReceipt": false,
       "IsApprovementSignature": false,
       "IsEncryptedContent": false
   }

SDK
---

Пример кода на C# для отправки счета-фактуры:

.. code-block:: csharp

	//Для работы с документами в Диадоке необходим авторизационный токен.
	//Подробнее о получении авторизационного токена можно узнать в разделе "Как авторизоваться в системе".
	public static string AuthTokenCert;
	
	public static string BoxId = "идентификатор ящика отправителя";
	
	//Формирование счета-фактуры
	public static GeneratedFile GenerateInvoiceXml()
	{
		var content = new InvoiceInfo()
		{
			//Заполняется согласно структуре InvoiceInfo
		};
		return Api.GenerateInvoiceXml(AuthTokenCert, content);
	}
		
	//Отправка счета-фактуры
	public static Message SendInvoiceXml()
	{
		var invoice = GenerateInvoiceXml();
		var messageAttachment = new XmlDocumentAttachment
		{
			SignedContent = new SignedContent
			{
				Content = invoice.Content,
				//Подпись отправителя, см. "Как авторизоваться в системе"
				Signature = Crypt.Sign(invoice.Content, ReadCertContent("путь к сертификату"))
			}
		};
		var messageToPost = new MessageToPost
		{
			FromBoxId = BoxId,
			ToBoxId = "идентификатор ящика получателя",
			Invoices = 
			{ 
				messageAttachment 
			}
		};
		return Api.PostMessage(AuthTokenCert, messageToPost);
	}
	
	//Получение подтверждения оператора, формирование и отправка извещения о получении 
	public static void GetInvoiceConfirmationAndSendReceipt(Message invoiceMessage)
	{
		var confirmationEntityId = "";

		foreach (var entity in invoiceMessage.Entities)
		{
			if (entity.AttachmentType == AttachmentType.InvoiceConfirmation)
			{
				confirmationEntityId = entity.EntityId;
				break;				
			}
		}
		
		var receipt = Api.GenerateInvoiceDocumentReceiptXml(AuthTokenCert, BoxId, invoiceMessage.MessageId, confirmationEntityId, new Signer()
		{
			//Подпись отправителя, см. "Как авторизоваться в системе"
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
				//Подпись отправителя, см. "Как авторизоваться в системе"
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
	
	//Получение извещения о получении счета-фактуры
	public static byte[] GetInvoiceReceipt(Message invoiceMessage)
	{
		var receiptEntityId = "";
		foreach (var entity in invoiceMessage.Entities)
		{
			if (entity.AttachmentType == AttachmentType.InvoiceReceipt &&
				entity.ParentEntityId == invoiceMessage.Entities[0].EntityId)
				receiptEntityId = entity.EntityId;
		}
		return Api.GetEntityContent(AuthTokenCert, BoxId, invoiceMessage.MessageId, receiptEntityId); 
	}
	
	public static void Main()
	{
		var invoiceMessage = SendInvoiceXml();
		
		//Оператор формирует подтверждение в течение нескольких секунд.
		//Для получения сообщения с подтверждением необходимо вызвать метод GetMessage()
		var invoiceMessageWithConfirmation = Api.GetMessage(AuthTokenCert, BoxId, invoiceMessage.MessageId);
		
		GetInvoiceConfirmationAndSendReceipt(invoiceMessageWithConfirmation);
		
		//Технический документ можно получить в виде массива байтов.
		//Для получения сообщения с новыми вложениями необходимо снова вызвать метод GetMessage()
		var invoiceMessageWithReceipt = Api.GetMessage(AuthTokenCert, BoxId, invoiceMessage.MessageId);
		var invoiceMessageWithReceipt = Api.GetMessage(AuthTokenCert, BoxId, invoiceMessage.MessageId);
		
		//Технический документ можно получить в виде массива байтов.
		var invoiceReceipt = GetInvoiceReceipt(invoiceMessageWithReceipt);
	}