Как отправить счет-фактуру
==========================

Рассмотрим последовательность действий к функциям интеграторского интерфейса Диадока, которые требуется совершить продавцу при отправке счета-фактуры (СФ), корректировочного счета-фактуры (КСФ), исправления счета-фактуры (ИСФ).

Порядок согласно приказу `N 14Н <https://normativ.kontur.ru/document?moduleId=1&documentId=385831>`_
------------------------------------------------------------------------------------------------------

Порядок документооборота со стороны продавца:

#. Продавец формирует счет-фактуру, подписывает и направляет Покупателю.

#. Диадок формирует подтверждение оператора о дате получения счета-фактуры, подписывает его и направляет Продавцу.

#. Продавец получает подтверждение оператора.

#. Продавец получает извещение о получении счета-фактуры от Покупателя.


.. note:: Более подробно о порядке обмена электронными счетами-фактурами между компаниями можно почитать в :doc:`соответствующем разделе <../docflows/InvoiceDocflow>` или на `сайте <http://www.diadoc.ru/docs/e-invoice/interchange>`__

.. _create_invoice:

Формирование счета-фактуры
~~~~~~~~~~~~~~~~~~~~~~~~~~

Если на стороне интеграционного решения не предусмотрено функциональности для формирования XML-документов, соответствующих утвержденным форматам, то продавец может сгенерировать СФ/ИСФ/КСФ/ИКСФ, используя метод :doc:`../http/GenerateTitleXml`.

В теле запроса должен содержаться упрощенный XML-файл, соответствующий XSD-схеме контракта для генерации титула.
XSD-схема контракта, необходимого для генерации титула, может быть получена с помощью ссылки, доступной в поле *UserDataXsdUrl* контракта :doc:`DocumentTitle <../proto/DocumentTypeDescription>`, который можно получить с помощью метода-справочника :doc:`GetDocumentTypes`.

В теле ответа содержится сгенерированный XML-файл титула, построенный на основании данных из запроса. Файл изготавливается в соответствии с XSD-схемой соответствующего титула документа.

Подробнее см. Обобщенный метод генерации :doc:`../http/GenerateTitleXml`.

.. _send_invoice:

Отправка счета-фактуры
~~~~~~~~~~~~~~~~~~~~~~

После того, как у вас есть XML-файл СФ/ИСФ/КСФ/ИКСФ, его нужно отправить с помощью метода :doc:`../http/PostMessage`.

Для этого нужно подготовить структуру :doc:`../proto/MessageToPost` следующим образом:

-  в значение атрибута *FromBoxId* указываем идентификатор ящика отправителя,

-  в значение атрибута *ToBoxId* указываем идентификатор ящика получателя,

-  для передачи XML-файла СФ/ИСФ/КСФ/ИКСФ нужно использовать атрибут *DocumentAttachments*, описываемый структурой *DocumentAttachment*

	-  внутри структуры *DocumentAttachment* находится вложенная структура *SignedContent*. Сам XML-файл нужно передать в атрибут *Content*, подпись продавца в атрибут *Signature*,
	-  внутри структуры *DocumentAttachment* в атрибут *TypeNamedId* нужно передать строковой идентификатор типа документа.

Описание структур, используемых при отправке СФ/ИСФ/КСФ/ИКСФ:

.. code-block:: protobuf

    message MessageToPost {
        required string FromBoxId = 1;
        optional string ToBoxId = 2;
        repeated DocumentAttachment DocumentAttachments = 34;
    }

    message DocumentAttachment {
        required SignedContent SignedContent = 1;
        optional string Comment = 3;
	required string TypeNamedId = 12;
    }

    message SignedContent {
        optional bytes Content = 1;
        optional bytes Signature = 2;
    }

После отправки в теле ответа будет содержаться отправленное сообщение, сериализованное в протобуфер :doc:`../proto/Message`.

.. _receive_confirmation_seller:

Получение подтверждения оператора
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

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

.. _receive_receipt:

Получение извещения о получении счета-фактуры
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

На отправленный счет-фактуру нужно получить извещение о получении счета-фактуры со стороны покупателя :doc:`InvoiceReceipt <../proto/Entity message>`.

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
~~~~~~~~~~~~~~~~~~

Пример кода на C# для отправки счета-фактуры:

.. code-block:: csharp

	//Для работы с документами в Диадоке необходим авторизационный токен.
	//Подробнее о получении авторизационного токена можно узнать в разделе "Как авторизоваться в системе".
	public static string AuthTokenCert;

	public static string BoxId = "идентификатор ящика отправителя";

	//Формирование счета-фактуры
	public static GeneratedFile GenerateInvoiceXml()
	{
	    var content = new InvoiceInfo();
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

	//Получение извещения о получении счета-фактуры
	public static byte[] GetInvoiceReceipt(Message invoiceMessage)
	{
	    var receiptEntityId = "";
	    foreach (var entity in invoiceMessage.Entities)
	    {
		if (entity.AttachmentType == AttachmentType.InvoiceReceipt && entity.ParentEntityId == invoiceMessage.Entities[0].EntityId)
		{
		    receiptEntityId = entity.EntityId;
		}
	    }

	    return Api.GetEntityContent(AuthTokenCert, BoxId, invoiceMessage.MessageId, receiptEntityId);
	}

	public static void Main()
	{
	    var invoiceMessage = SendInvoiceXml();

	    //Оператор формирует подтверждение в течение нескольких секунд.
	    //Для получения сообщения с подтверждением необходимо вызвать метод GetMessage()
	    var invoiceMessageWithConfirmation = Api.GetMessage(AuthTokenCert, BoxId, invoiceMessage.MessageId);

	    //Технический документ можно получить в виде массива байтов.
	    //Для получения сообщения с новыми вложениями необходимо снова вызвать метод GetMessage()
	    var invoiceMessageWithReceipt = Api.GetMessage(AuthTokenCert, BoxId, invoiceMessage.MessageId);

	    //Технический документ можно получить в виде массива байтов.
	    var invoiceReceipt = GetInvoiceReceipt(invoiceMessageWithReceipt);
	}

Порядок согласно приказу `N 174Н <https://normativ.kontur.ru/document?moduleId=1&documentId=268278>`_ (утратил силу с 01.07.2021)
------------------------------------------------------------------------------------------------------

.. raw:: html

   <details>
   <summary><a>Подробнее</a></summary>

Порядок документооборота со стороны продавца:

#. Продавец формирует счет-фактуру, подписывает и направляет Покупателю.

#. Диадок формирует подтверждение оператора о дате получения счета-фактуры, подписывает его и направляет Продавцу.

#. Продавец получает подтверждение оператора и отправляет в ответ подписанное извещение о получении подтверждения.

#. Продавец получает извещение о получении счета-фактуры от Покупателя.

Формирование счета-фактуры
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Действия аналогичны инструкции для обмена СФ по 14Н (см. :ref:`create_invoice`).

Отправка счета-фактуры
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Действия аналогичны инструкции для обмена СФ по 14Н (см. :ref:`send_invoice`).

Получение подтверждения оператора
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Действия аналогичны инструкции для обмена СФ по 14Н (см. :ref:`receive_confirmation_seller`).

Формирование извещения о получении подтверждения оператора
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

После того, как продавец получил подтверждение оператора, он должен отправить в ответ подписанное извещение :doc:`InvoiceReceipt  <../proto/Entity message>` о получении подтверждения.

Извещение о получении подтверждения оператора представляется структурой :doc:`Entity <../proto/Entity message>`, где значение полей ``EntityType`` и ``AttachmentType`` должно быть *Attachment/InvoiceReceipt*.

В API Диадока есть метод, который позволяет сформировать извещение о получении подтверждения оператора - :doc:`../http/GenerateReceiptXml`, при вызове этого метода нужно корректно указать GET-параметры ``boxId``, ``messageId``, ``attachmentId`` и передать в тело запроса данные о подписанте генерируемого извещения в виде сериализованной структуры :doc:`../proto/Signer`.

``BoxId`` - это идентификатор ящика отправителя, ``messageId`` - идентификатор отправленного сообщения с СФ/ИСФ/КСФ/ИКСФ, ``attachmentId`` - идентификатор подтверждение оператора. Их можно взять из структуры :doc:`../proto/Message`.

Например, HTTP-запрос для формирования извещение о получении подтверждения оператора выглядит следующим образом:

::

    POST /GenerateReceiptXml?boxId=db32772b-9256-49a8-a133-fda593fda38a&messageId=a9093c56-7c48-4ab1-bc87-efb04e7d4400&attachmentId=f80738a3-b0bc-426a-aadf-6967ec1b53df HTTP/1.1
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
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

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
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Действия аналогичны инструкции для обмена СФ по 14Н (см. :ref:`receive_receipt`).

SDK
~~~~~~~~~~~~

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

		var receipt = Api.GenerateReceiptXml(AuthTokenCert, BoxId, invoiceMessage.MessageId, confirmationEntityId, new Signer()
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

.. raw:: html

   </details>
