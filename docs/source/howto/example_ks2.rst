Как отправить и получить акт о приемке выполненных работ КС-2 в рекомендованном ФНС формате
===========================================================================================

Рассмотрим сценарий работы с актом о приемке выполненных работ КС-2.

#. Подрядчик формирует файл титула подрядчика акта о приемке выполненных работ, подписывает и направляет заказчику.

#. Заказчик получает акт о приемке выполненных работ, подписанный и отправленный подрядчиком.

#. Заказчик формирует файл титула заказчика, подписывает своей ЭП и отправляет в адрес подрядчика.

.. note::
	Согласно формату справка КС-3 — это всегда дополнение к акту КС-2, она не может быть оформлена отдельно. При выполнении условия «НастрФормДок.ПрНакИтог == 1 ИЛИ 2» и «НастрФормДок.ПрСведРасчСогл == 1», документ содержит данные для КС-3. 


Формирование файла титула подрядчика для акта о приемке выполненных работ КС-2
-----------------------------------------------------------------------------------

Файлы титулов акта о приемке выполненных работ КС-2 нужно сформировать в сторонней информационной системе. Генерация в АПИ Диадока недоступна.

Отправка файла титула подрядчика для акта о приемке выполненных работ КС-2
-------------------------------------------------------------------------------

Титул подрядчика можно отправить с помощью метода :doc:`../http/PostMessage`. 

Для этого подготовьте структуру :doc:`../proto/MessageToPost`:

- в поле ``FromBoxId`` укажите идентификатор ящика отправителя;
- в поле ``ToBoxId`` укажите идентификатор ящика получателя;
- для передачи XML-файла титула подрядчика акта КС-2 используйте вложенную структуру ``DocumentAttachment``:

	- XML-файл передайте в структуре ``SignedContent`` в поле ``Content``, подпись — в поле ``Signature``,
	- ``TypeNamedId=PerformedWorkAcceptanceCertificate``,
	- ``Function=default``,	
	- ``Version=performedworkacceptancecertificate691_01_00_01``.

Описание структур, используемых при отправке акта КС-2:

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

Все дальнейшие действия происходят на стороне заказчика.

Поиск и получение акта КС-2
---------------------------

Чтобы найти все входящие акты КС-2, которые нужно обработать, используйте метод :doc:`../http/GetDocuments`:

- в поле ``boxId`` укажите идентификатор ящика, в котором нужно найти входящие документы;
- в поле ``filterCategory`` укажите статус и тип документа: ``PerformedWorkAcceptanceCertificate.InboundNotFinished``.

Пример запроса на получение акта КС-2:

::

    GET /V3/GetDocuments?filterCategory=PerformedWorkAcceptanceCertificate.InboundNotFinished&boxId=db32772b-9256-49a8-a133-fda593fda38a HTTP/1.1
    Host: diadoc-api.kontur.ru
    Accept: application/json
    Content-Type: application/json charset=utf-8
    Authorization: DiadocAuth ddauth_api_client_id={{ключ разработчика}}, ddauth_token={{авторизационный токен}}

В теле ответа вернется список документов в виде структуры ``DocumentList`` с вложенной структурой ``Document``. Чтобы получить документы, потребуются значения полей ``MessageId`` и ``EntityId``.

Чтобы получить акт КС-2, вызовите метод :doc:`../http/GetMessage` и укажите нужные GET-параметры ``boxId``, ``messageId``, ``entityId``.

::

    GET /V3/GetMessage?messageId=bbcedb0d-ce34-4e0d-b321-3f600c920935&entityId=30cf2c07-7297-4d48-bc6f-ca7a80e2cf95&boxId=db32772b-9256-49a8-a133-fda593fda38a HTTP/1.1
    Host: diadoc-api.kontur.ru
    Accept: application/json
    Content-Type: application/json charset=utf-8
    Authorization: DiadocAuth ddauth_api_client_id={{ключ разработчика}}, ddauth_token={{авторизационный токен}}

Отправка файла титула заказчика акта КС-2
-----------------------------------------

Отправить титул можно с помощью метода :doc:`../http/PostMessagePatch`. 

Для этого подготовьте структуру :doc:`../proto/MessagePatchToPost`:

- в значение атрибута ``BoxId`` укажите идентификатор ящика, в котором находится исходное сообщение,
- в значение атрибута ``MessageId`` укажите идентификатор сообщения, к которому относится дополнение,
- чтобы передать XML-файла титула, используйте структуру ``RecipientTitleAttachment``:

	- ``ParentEntityId`` — идентификатор титула подрядчика,
	- XML-файл нужно передать во вложенной структуре ``SignedContent`` в поле ``Content``, подпись — в поле ``Signature``.

Описание структур, используемых при отправке ответного титула акта КС-2:

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