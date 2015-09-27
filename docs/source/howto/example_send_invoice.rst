Как отправить счет-фактуру
==========================

Рассмотрим последовательность действий к функциям интеграторского интерфейса Диадока, которые требуется совершить продавцу при отправке счета-фактуры (СФ), корректировочного счета-фактуры (КСФ), исправления счета-фактуры (ИСФ).

#. Продавец должен сформировать счет-фактуру, подписать и направить Покупателю.

#. Диадок должен сормировать подтверждение оператора о дате отправки счета-фактуры, подписать его и направить Продавцу.

#. Продавец должен получить подтверждение оператора и отправить в ответ подписанное извещение о получении подтверждения.


.. note:: Более подробно о порядке обмена электронными счетами-фактурами между компаниями можно почитать в :doc:`соответствующем разделе <../InvoiceDocflow>` или на `сайте <http://www.diadoc.ru/docs/e-invoice/interchange>`__

Формирование счета-фактуры
--------------------------

Если на стороне интеграционного решения не предусмотрено функциональности для формирования XML-документов, соответствущих утвержденным форматам, то продавец должен сгенерировать СФ/ИСФ/КСФ/ИКСФ, используя команду :doc:`../http/GenerateInvoiceXml`.

Для формирования СФ в GET-параметр ``invoiceType`` нужно передать значение ``Invoice``.
	   
В теле запроса должны содержаться данные для изготовления СФ/ИСФ/КСФ/ИКСФ:
	
	-  в виде сериализованной структуры :doc:`../proto/InvoiceInfo` для типов документов ``Invoice`` или ``InvoiceRevision``
	
	-  в виде сериализованной структуры :doc:`../proto/InvoiceCorrectionInfo` для типов документов ``InvoiceCorrection`` или ``InvoiceCorrectionRevision``.
	   
Например HTTP-запрос для генерации СФ выглядит следующим образом:

::

    POST https://diadoc-api.kontur.ru/GenerateInvoiceXml?invoiceType=Invoice HTTP/1.1
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

Файл СФ/ИСФ изготавливается в соответствии с `XML-схемой <https://diadoc.kontur.ru/sdk/xsd/ON_SFAKT_1_897_01_05_02_01.xsd>`__, которой должны удовлетворять XML-счета-фактуры, согласно приказу ФНС.

Файл КСФ/ИКСФ изготавливается в соответствии с другой утвержденной ФНС `XML-схемой <https://diadoc.kontur.ru/sdk/xsd/ON_KORSFAKT_1_911_01_05_02_01.xsd>`__. 

Имя файла СФ/ИСФ/КСФ/ИКСФ (формат которого также определяет приказ ФНС) возвращается в стандартном HTTP-заголовке ``Content-Disposition``.

Отправка счета-фактуры
----------------------

После того, как у вас есть XML-файл СФ/ИСФ/КСФ/ИКСФ, его нужно отправить с помощью команды :doc:`../http/PostMessage`. 

Для этого нужно подготовить структуру :doc:`../proto/MessageToPost` следующим образом:

-  в значение атрибута *FromBoxId* указываем идентификатор ящика отправителя,

-  в значение атрибута *ToBoxId* указываем идентификатор ящика получателя

-  для передачи XML-файла СФ/ИСФ/КСФ/ИКСФ нужно использовать атрибут *Invoices*, описываемый структурой *XmlDocumentAttachment*

	-  внутри структуры *XmlDocumentAttachment* находится вложенная структура *SignedContent*,
	
	-  сам XML-файла нужна передать в атрибут *Content*, подпись продавца в атрибут *Signature*
	   
Описание структур, используемых при отправке СФ:

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

После отправки в теле ответа будет содержатся отправленное сообщение, сериализованное в протобуфер :doc:`../proto/Message`.

Получение подтверждения
-----------------------

После успешной отправки СФ необходимо получить подтверждение оператора :doc:`InvoiceConfirmation <../proto/Entity message>`.

Подтверждение оператора представляется структуру :doc:`Entity <../proto/Entity message>`, где значение полей ``EntityType`` и ``AttachmentType`` должно быть *Attachment/InvoiceConfirmation*.

Чтобы получить подтверждение оператора нужно вызвать метод :doc:`../http/GetMessage` и указать нужные GET-параметры ``boxId``, ``messageId``, ``entityId``.

``BoxId`` - это идентификатор ящика отправителя, ``messageId`` - идентификатор отправленного сообщения с СФ, ``entityId`` - идентификатор счета-фактуры. Их можно взять из структуры :doc:`../proto/Message`

Например HTTP-запрос для получения сообщения выглядит следующим образом:

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

Формирование извещения
----------------------

После успешной отправки необходимо получить подтверждение оператора :doc:`InvoiceConfirmation <../proto/Entity message>` и отправить в ответ извещение о получении данного подтверждения :doc:`InvoiceReceipt <../proto/Entity message>`.

Извещение о получении данного подтверждения представляется структуру :doc:`Entity <../proto/Entity message>`, где  значение полей ``EntityType`` и ``AttachmentType`` должно быть *Attachment/InvoiceReceipt*.
