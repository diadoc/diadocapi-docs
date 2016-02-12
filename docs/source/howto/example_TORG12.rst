Как отправить и получить товарную накладную ТОРГ-12 в рекомендованном ФНС формате
=================================================================================

Рассмотрим последовательность действий к функциям интеграторского интерфейса Диадока, которые требуется совершить при отправке товарной накладной ТОРГ-12.

#. Продавец формирует файл титула продавца, подписывает и направляет покупателю.

#. Покупатель получает товарную накладную, подписанную и отправленную продавцом;

#. Покупатель формирует файл титула покупателя, подписывает своей ЭП и отправляет в адрес продавца.


.. note:: Более подробно о порядке обмена электронными накладными между компаниями можно почитать на `сайте <http://www.diadoc.ru/docs/others/tn>`__

Формирование файла титула продавца для товарной накладной ТОРГ-12
-----------------------------------------------------------------

Если на стороне интеграционного решения не предусмотрено функциональности для формирования XML-документов, соответствущих утвержденным форматам, то продавец может сгенерировать файл титула, используя команду :doc:`../http/GenerateTorg12XmlForSeller`.
	   
В теле запроса должны содержаться данные для изготовления титула продавца для товарной накладной ТОРГ-12 в XML-формате в виде сериализованной структуры :doc:`Torg12SellerTitleInfo <../proto/Torg12Info>`.
	   
HTTP-запрос для генерации файла титула продавца товарной накладной ТОРГ-12 выглядит следующим образом:

::

    POST /GenerateTorg12XmlForSeller HTTP/1.1
    Host: diadoc-api.kontur.ru
    Authorization: DiadocAuth ddauth_api_client_id=testClient-8ee1638deae84c86b8e2069955c2825a
    Content-Length: 1252
    Connection: Keep-Alive

    <Сериализованная структура Torg12SellerTitleInfo>

В теле ответа содержится XML-файл титула продавца, построенный на основании данных из запроса.

Успешный ответ сервера выглядит так:
::

    HTTP/1.1 200 OK
    Content-Length: 598

    <XML-файл титула продавца>

Файл генерируется в соответствии с `XML-схемой <https://diadoc.kontur.ru/sdk/xsd/DP_OTORG12_1_986_00_05_01_02.xsd>`__, которой должны удовлетворять XML-накладные, согласно приказу ФНС.


Имя файла титула продавца для товарной накладной возвращается в стандартном HTTP-заголовке ``Content-Disposition``.

Отправка файла титула продавца для товарной накладной ТОРГ-12
-------------------------------------------------------------

После того, как у вас есть XML-файл титула продавца, его нужно отправить с помощью команды :doc:`../http/PostMessage`. 

Для этого нужно подготовить структуру :doc:`../proto/MessageToPost` следующим образом:

-  в значение атрибута *FromBoxId* указываем идентификатор ящика отправителя;

-  в значение атрибута *ToBoxId* указываем идентификатор ящика получателя;

-  для передачи XML-файла титула продавца товарной накладной ТОРГ-12 нужно использовать атрибут *XmlTorg12SellerTitles*, описываемый структурой *XmlDocumentAttachment*:

	-  внутри структуры *XmlDocumentAttachment* находится вложенная структура *SignedContent*;
	
	-  сам XML-файл нужно передать в атрибут *Content*, подпись продавца в атрибут *Signature*.
	   
Описание структур, используемых при отправке товарной накладной ТОРГ-12:

.. code-block:: protobuf

    message MessageToPost {
        required string FromBoxId = 1;
        optional string ToBoxId = 2;
        repeated XmlDocumentAttachment XmlTorg12SellerTitles = 3;
    }

    message XmlDocumentAttachment {
        required SignedContent SignedContent = 1;
    }

    message SignedContent {
        optional bytes Content = 1;
        optional bytes Signature = 2;
    }

После отправки в теле ответа будет содержаться отправленное сообщение, сериализованное в протобуфер :doc:`../proto/Message`.

Все дальнейшие действия происходят на стороне покупателя.

Поиск товарной накладной ТОРГ-12
--------------------------------

Сначала покупателю необходимо найти все входящие товарные накладные ТОРГ-12, которые требуется обработать. Для этого нужно воспользоваться методом :doc:`../http/GetDocuments`:

  -  в значении параметра *boxId* указываем идентификатор ящика, в котором следует выполнить поиск входящих документов;

  -  в параметр *filterCategory* указываем статус и тип документа: ``XmlTorg12.InboundNotFinished``.

Пример запроса на получение товарной накладной ТОРГ-12 выглядит следующим образом:

::

    GET /V3/GetDocuments?filterCategory=XmlTorg12.InboundNotFinished&boxId=db32772b-9256-49a8-a133-fda593fda38a HTTP/1.1
    Host: diadoc-api.kontur.ru
    Accept: application/json
    Content-Type: application/json charset=utf-8
    Authorization: DiadocAuth ddauth_api_client_id=testClient-87e1638deae84c86b8e2069955c2825a0987

В теле ответа вернется список документов в виде структуры *DocumentList* с вложенной структурой *Document*. Для каждого из этих документов запоминаем: *MessageId*, *EntityId*.

Получение товарной накладной ТОРГ-12
------------------------------------

Теперь необходимо получить найденную товарную накладную :doc:`XmlTorg12 <../proto/Entity message>`.

Чтобы получить товарную накладную ТОРГ-12 нужно вызвать метод :doc:`../http/GetMessage` и указать нужные GET-параметры ``boxId``, ``messageId``, ``entityId``.

``BoxId`` - это идентификатор ящика получателя, ``messageId`` - идентификатор полученного сообщения с накладной ТОРГ-12, ``entityId`` - идентификатор товарной накладной. Их можно взять из структуры :doc:`../proto/Message`.

.. code-block:: json

    GET /V3/GetMessage?messageId=bbcedb0d-ce34-4e0d-b321-3f600c920935&entityId=30cf2c07-7297-4d48-bc6f-ca7a80e2cf95&boxId=db32772b-9256-49a8-a133-fda593fda38a HTTP/1.1
    Host: diadoc-api.kontur.ru
    Accept: application/json
    Content-Type: application/json charset=utf-8
    Authorization: DiadocAuth ddauth_api_client_id=testClient-87e1638deae84c86b8e2069955c2825a0987

Пример структуры товарной накладной ТОРГ-12 :doc:`XmlTorg12 <../proto/Entity message>` в теле ответа:

.. code-block:: json

   {
       "EntityType": "Attachment",
       "EntityId": "654ac483-0dd4-4085-b70f-565c8b754e10",
       "Content": "lores ipsum",
       "AttachmentType": "XmlTorg12",
       "FileName": "DP_OTORG12_2BM-7750370234-4012052808304878702630000000000_2BM_20150927_324c290e-f049-4906-baac-1ddcd7f3c2ff.xml",
       "NeedRecipientSignature": true,
       "SignerBoxId": "",
       "NotDeliveredEventId": "",
       "RawCreationDate": 635789700936777240,
       "SignerDepartmentId": "",
       "NeedReceipt": false,
       "IsApprovementSignature": false,
       "IsEncryptedContent": false
   }

.. _create_receipt:

Формирование файла титула покупателя для товарной накладной ТОРГ-12
-------------------------------------------------------------------

Файл титула покупателя можно сформировать как на стороне интеграционного решения, так и используя команду :doc:`../http/GenerateTorg12XmlForBuyer`. Для этого надо передать следующие параметры: 

- ``boxId`` - идентификатор ящика получателя;

- ``sellerTitleMessageId`` - идентификатор сообщения, содержащего соответствующий титул продавца;

- ``sellerTitleAttachmentId`` - идентификатор сущности, представляющей титул продавца, для которого требуется изготовить титул покупателя.

Эти идентификаторы соответствуют идентификаторам из параметров ``boxId``, ``messageId``, ``entityId`` для метода :doc:`../http/GetMessage`.
	   
В теле запроса должны содержаться данные для изготовления титула покупателя для товарной накладной ТОРГ-12 в XML-формате в виде сериализованной структуры :doc:`Torg12BuyerTitleIhfo <../proto/Torg12Info>`.
	   
HTTP-запрос для генерации файла титула покупателя товарной накладной ТОРГ-12 выглядит следующим образом:

::

    POST /GenerateTorg12XmlForBuyer?sellerTitleMessageId=bbcedb0d-ce34-4e0d-b321-3f600c920935&sellerTitleAttachmentId=30cf2c07-7297-4d48-bc6f-ca7a80e2cf95&boxId=db32772b-9256-49a8-a133-fda593fda38a HTTP/1.1
    Host: diadoc-api.kontur.ru
    Authorization: DiadocAuth ddauth_api_client_id=testClient-8ee1638deae84c86b8e2069955c2825a
    Content-Length: 1252
    Connection: Keep-Alive

    <Сериализованная структура Torg12BuyerTitleInfo>

В теле ответа содержится XML-файл титула покупателя, построенный на основании XML-файла титула продавци и данных из запроса.

Успешный ответ сервера выглядит так:
::

    HTTP/1.1 200 OK
    Content-Length: 598

    <XML-файл титула покупателя>

Файл генерируется в соответствии с `XML-схемой <https://diadoc.kontur.ru/sdk/xsd/DP_OTORG12_1_986_00_05_01_02.xsd>`__, которой должны удовлетворять XML-накладные, согласно приказу ФНС.


Имя файла титула покупателя для товарной накладной возвращается в стандартном HTTP-заголовке ``Content-Disposition``.

Отправка файла титула покупателя для товарной накладной ТОРГ-12
---------------------------------------------------------------
После того, как у вас есть XML-файл титула покупателя, его нужно отправить с помощью команды :doc:`../http/PostMessagePatch`. 

Для этого нужно подготовить структуру :doc:`../proto/MessagePatchToPost` следующим образом:

-  в значение атрибута *BoxId* указываем идентификатор ящика, в котором находится исходное сообщение;

-  в значение атрибута *MessageId* указываем идентификатор сообщения, к которому относится отправляемый патч;

-  для передачи XML-файла титула продавца товарной накладной ТОРГ-12 нужно использовать атрибут *XmlTorg12BuyerTitles*, описываемый структурой *ReceiptAttachment*:

    -  ParentEntityId - идентификатор документа, к которому относится титул покупателя; это идентификатор соответствующей сущности из родительского сообщения (поле EntityId в структуре :doc:`Entity <../proto/Entity message>`.);

	-  внутри структуры *ReceiptAttachment* находится вложенная структура *SignedContent*;
	
	-  сам XML-файл нужно передать в атрибут *Content*, подпись продавца в атрибут *Signature*.
	   
Описание структур, используемых при отправке товарной накладной ТОРГ-12:

.. code-block:: protobuf

    message MessagePatchToPost {
        required string BoxId = 1;
        optional string MessageId = 2;
        repeated ReceiptAttachment XmlTorg12BuyerTitles = 7;
    }

    message ReceiptAttachment {
		required string ParentEntityId = 1;
        required SignedContent SignedContent = 1;
    }

    message SignedContent {
        optional bytes Content = 1;
        optional bytes Signature = 2;
    }

После отправки в теле ответа будет содержаться отправленное дополнение, сериализованное в протобуфер :doc:`../proto/MessagePatch`.

SDK
---

Пример кода на C# для отправки файла титула продавца для товарной накладной ТОРГ-12:

.. code-block:: csharp

	// формирование файла титула продавца
	private GeneratedFile GenerateTorg12SellerTitle()
	{
		var content = new Torg12SellerTitleInfo()
			{
				// заполняем согласно структуре Torg12SellerTitleInfo
			};
		return api.GenerateTorg12XmlForSeller(authToken, content);
	}
		
	// отправка файла титула продавца
	private void SendTorg12SellerTitle()
	{
		var fileToSend = GenerateTorg12SellerTitle();

		var messageAttachment = new XmlDocumentAttachment
		{
			SignedContent = new SignedContent //файл подписи
			{
				Content = fileToSend.Content,
				Signature = new byte[0] //подпись продавца
			}
		};

		var messageToPost = new MessageToPost
		{
			FromBoxId = "идентификатор ящика отправителя",
			ToBoxId = "идентификатор ящика получателя",
			XmlTorg12SellerTitles = { messageAttachment }
		};

		api.PostMessage(authToken, messageToPost); //см. "Как авторизоваться в системе"
	}

	
Пример кода на C# для получения файла титула продавца для товарной накладной ТОРГ-12 и отправки файла титула покупателя:

.. code-block:: csharp

	//находим все неподписанные товарные накладные ТОРГ-12
	private Document SearchTorg12Documents()
	{
		var boxId = "идентификатор ящика, в котором следует выполнить поиск входящих документов";
			
		//статус и тип документа
		var filterCategory = "XmlTorg12.InboundNotFinished"; 
		var counteragentBoxId = "идентификатор ящика контрагента";
			
		DocumentList documents = api.GetDocuments(authToken, boxId, filterCategory, counteragentBoxId);
			
		return documents.Documents.First();
	}
		
	//получаем нужную товарную накладную ТОРГ-12 и отправляем к ней титул покупателя
	private void GetTorg12AndSendTorg12BuyerTitle()
	{
		var document = SearchTorg12Documents();
		var boxId = "идентификатор ящика получателя";
			
		//получение товарной накладной ТОРГ-12
		var message = api.GetMessage(authToken, boxId, document.MessageId, document.EntityId); 
			
		//генерация файла титула покупателя
		var buyerInfo = GetBuyerInfo();
		
		//формирование файла титула покупателя
		var torg12XmlForBuyer = api.GenerateTorg12XmlForBuyer(authToken, buyerInfo, boxId, document.MessageId, document.EntityId);
	
		var messagePatchToPost = new MessagePatchToPost
		{
			BoxId = boxId,
			MessageId = document.MessageId,
			XmlTorg12BuyerTitles =
			{
				new ReceiptAttachment
				{
					ParentEntityId = document.EntityId,
					SignedContent = new SignedContent //файл подписи
					{
						Content = document.Content,
						Signature = new byte[0] //подпись покупателя
					}
				}
			}
		};

		api.PostMessagePatch(authToken, messagePatchToPost);
	}
	
	//генерация файла титула покупателя
	private Torg12BuyerTitleInfo GetBuyerInfo()
	{
		return new Torg12BuyerTitleInfo
		{
			//заполняется согласно структуре Torg12BuyerTitleInfo
		};
	}