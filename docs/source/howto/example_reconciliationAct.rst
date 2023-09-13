Как отправить и получить акт сверки взаимных расчетов в рекомендованном ФНС формате
===================================================================================

Сценарий работы с актом сверки взаимных расчетов
------------------------------------------------

#. Отправитель формирует файл титула отправителя, подписывает и направляет получателю.

#. Получатель получает файл титула отправителя, подписанный и отправленный отправителем.

#. Получатель формирует файл титула получателя, подписывает своей ЭП и отправляет в ответ к файлу титула отправителя. Через API Диадока можно отправить титул получателя с разногласиями.


Формирование файла титула отправителя для акта сверки взаимных расчетов
-----------------------------------------------------------------------
Если на стороне интеграционного решения нельзя сформировать XML-документ, соответствущий утвержденному формату, то отправитель может сгенерировать файл титула с помощью метода :doc:`../http/GenerateTitleXml`.

Отправка файла титула отправителя для акта сверки взаимных расчетов
-------------------------------------------------------------------

Титул отправителя можно отправить с помощью метода :doc:`../http/PostMessage`. 

Для этого подготовьте структуру :doc:`../proto/MessageToPost`:

- в поле ``FromBoxId`` укажите идентификатор ящика отправителя;
- в поле ``ToBoxId`` укажите идентификатор ящика получателя;
- для передачи XML-файла титула отправителя акта сверки используйте вложенную структуру ``DocumentAttachment``:

	- XML-файл передайте в структуре ``SignedContent`` в поле ``Content``, подпись — в поле ``Signature``;
	- ``TypeNamedId=ReconciliationAct``;
	- ``Function=default``;
	- ``Version=reconciliationact405_05_01_01``.

Описание структур, используемых при отправке титула отправителя акта сверки:

.. code-block:: protobuf

    message MessageToPost {
        required string FromBoxId = 1;
        optional string ToBoxId = 2;
        repeated DocumentAttachment DocumentAttachments = 34;
    }

    message DocumentAttachment {
     required SignedContent SignedContent = 1;
     required string TypeNamedId = 12;
     optional string Function = 13;
     optional string Version = 14; 
    }

    message SignedContent {
        optional bytes Content = 1;
        optional bytes Signature = 2;
    }

После отправки в теле ответа будет содержаться отправленное сообщение, сериализованное в протобуфер :doc:`../proto/Message`.

Все дальнейшие действия происходят на стороне получателя.

Получение файла титула отправителя для акта сверки взаимных расчетов
--------------------------------------------------------------------

Перед получением файла титула отправителя найдите все входящие акты сверки, которые нужно обработать. Для этого используйте метод :doc:`../http/GetDocuments`:

- в поле ``boxId`` укажите идентификатор ящика, в котором нужно найти входящие документы;
- в поле ``filterCategory`` укажите статус и тип документа: ``ReconciliationAct.InboundNotFinished``.

Пример запроса на поиск акта сверки:

::

    GET /V3/GetDocuments?filterCategory=ReconciliationAct.InboundNotFinished&boxId=db32772b-9256-49a8-a133-fda593fda38a HTTP/1.1
    Host: diadoc-api.kontur.ru
    Accept: application/json
    Content-Type: application/json charset=utf-8
    Authorization: DiadocAuth ddauth_api_client_id={{ключ разработчика}}, ddauth_token={{авторизационный токен}}

В теле ответа вернется список документов в виде структуры ``DocumentList`` с вложенной структурой ``Document``. Чтобы получить документы, потребуются значения полей ``MessageId`` и ``EntityId``.

Чтобы получить акт сверки, вызовите метод :doc:`../http/GetMessage` и укажите GET-параметры: ``boxId``, ``messageId``, ``entityId``.

::

    GET /V3/GetMessage?messageId=bbcedb0d-ce34-4e0d-b321-3f600c920935&entityId=30cf2c07-7297-4d48-bc6f-ca7a80e2cf95&boxId=db32772b-9256-49a8-a133-fda593fda38a HTTP/1.1
    Host: diadoc-api.kontur.ru
    Accept: application/json
    Content-Type: application/json charset=utf-8
    Authorization: DiadocAuth ddauth_api_client_id={{ключ разработчика}}, ddauth_token={{авторизационный токен}}

Формирование файла титула получателя для акта сверки взаимных расчетов
----------------------------------------------------------------------

Файл титула получателя сведений можно сформировать как на стороне интеграционного решения, так и используя метод :doc:`../http/GenerateTitleXml`. 

Отправка файла титула получателя для акта сверки взаимных расчетов
------------------------------------------------------------------

Отправить титул получателя акта сверки можно с помощью метода :doc:`../http/PostMessagePatch`. 

Для этого подготовьте структуру :doc:`../proto/MessagePatchToPost`:

- в поле ``BoxId`` укажите идентификатор ящика, в котором находится исходное сообщение;
- в поле ``MessageId`` укажите идентификатор сообщения, к которому относится дополнение;
- чтобы передать XML-файла титула, используйте структуру ``RecipientTitleAttachment``:

	- ``ParentEntityId`` — идентификатор титула отправителя;
	- XML-файл нужно передать во вложенной структуре ``SignedContent`` в поле ``Content``, подпись — в поле ``Signature``.

Описание структур, используемых при отправке ответного титула акта сверки:

.. code-block:: protobuf

    message MessagePatchToPost {
        required string BoxId = 1;
        optional string MessageId = 2;
        repeated RecipientTitleAttachment RecipientTitles = 22;
    }

    message RecipientTitleAttachment  {
	required string ParentEntityId = 1;
        required SignedContent SignedContent = 1;
    }

    message SignedContent {
        optional bytes Content = 1;
        optional bytes Signature = 2;
    }

После отправки в теле ответа будет содержаться отправленное дополнение, сериализованное в протобуфер :doc:`../proto/MessagePatch`.