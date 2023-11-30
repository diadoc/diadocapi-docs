Как отправить и получить акт об установленном расхождении ТОРГ-2 в рекомендованном ФНС формате
==============================================================================================

Рассмотрим сценарий работы с актом об установленном расхождении ТОРГ-2.

#. Покупатель формирует файл титула покупателя, подписывает и направляет продавцу.

#. Продавец получает титул покупателя акта о расхождениях, подписанный и отправленный покупателем.

#. Продавец формирует файл титула доп сведений, подписывает своей ЭП и отправляет в адрес покупателя.


Формирование файла титула покупателя для акта об установленном расхождении ТОРГ-2
---------------------------------------------------------------------------------

Если на стороне интеграционного решения нельзя сформировать XML-документ, соответствущий утвержденному формату, то покупатель может сгенерировать файл титула с помощью метода :doc:`../http/GenerateTitleXml`.

Для генерации титула покупателя методом :doc:`../http/GenerateTitleXml` понадобятся:

		- ``documentTypeNamedId`` — тип документа;
		- ``documentFunction`` — функция документа;
		- ``documentVersion`` — версия документа;
		- ``titleIndex`` — идентификатор титула документа.

	В теле запроса нужно передать XML-файл ``UserDataXsd``, соответствующий XSD-схеме. ``UsedDataXsd`` содержит информацию для генерации титула, которую может заполнить только пользователь.

Получить тип, функцию, версию, идентификатор титула и ссылку на скачивание XSD-схемы можно с помощью метода :doc:`../http/GetDocumentTypes`. В ответе метод возвращает описание всех типов документов, доступных в ящике.

Ниже приведено тело ответа метода :doc:`../http/GetDocumentTypes`. Для упрощения из него удалены другие типы, функции, версии и информация о метаданных.

.. container:: toggle

  .. code-block:: protobuf

      {
        "Name": "Torg2",
        "Title": "Акт об установленном расхождении ТОРГ-2",
        "SupportedDocflows": [
          0
        ],
        "RequiresFnsRegistration": true,
        "Functions": [
            {
            "Name": "NoAdditionalInfo",
            "Versions": [
              {
                "Version": "torg2_05_01_01",
                "SupportsContentPatching": true,
                "SupportsEncrypting": false,
                "SupportsPredefinedRecipientTitle": false,
                "SupportsAmendmentRequest": true,
                "Titles": [
                  {
                    "Index": 0,
                    "IsFormal": true,
                    "XsdUrl": "/GetContent?typeNamedId=Torg2&function=NoAdditionalInfo&version=torg2_05_01_01&titleIndex=0&contentType=TitleXsd",
                    "UserDataXsdUrl": "/GetContent?typeNamedId=Torg2&function=NoAdditionalInfo&version=torg2_05_01_01&titleIndex=0&contentType=UserContractXsd",
                    "SignerInfo": {
                      "SignerType": 2,
                      "ExtendedDocumentTitleType": 9
                    },
                    "MetadataItems": [],
                    "EncryptedMetadataItems": []
                  }
               ],
               "IsActual": true,
                "Workflows": [
                  {
                   "Id": 1,
                    "IsDefault": true
                  }
                ]
              }
            ]
          },
          {
            "Name": "WithAdditionalInfo",
            "Versions": [
              {
                "Version": "torg2_05_01_01",
                "SupportsContentPatching": true,
                "SupportsEncrypting": false,
                "SupportsPredefinedRecipientTitle": false,
                "SupportsAmendmentRequest": true,
                "Titles": [
                  {
                    "Index": 0,
                    "IsFormal": true,
                    "XsdUrl": "/GetContent?typeNamedId=Torg2&function=WithAdditionalInfo&version=torg2_05_01_01&titleIndex=0&contentType=TitleXsd",
                    "UserDataXsdUrl": "/GetContent?typeNamedId=Torg2&function=WithAdditionalInfo&version=torg2_05_01_01&titleIndex=0&contentType=UserContractXsd",
                    "SignerInfo": {
                      "SignerType": 2,
                      "ExtendedDocumentTitleType": 9
                    },
                    "MetadataItems": [],
                    "EncryptedMetadataItems": []
                  },
                  {
                    "Index": 1,
                    "IsFormal": true,
                    "XsdUrl": "/GetContent?typeNamedId=Torg2&function=WithAdditionalInfo&version=torg2_05_01_01&titleIndex=1&contentType=TitleXsd",
                    "UserDataXsdUrl": "/GetContent?typeNamedId=Torg2&function=WithAdditionalInfo&version=torg2_05_01_01&titleIndex=1&contentType=UserContractXsd",
                    "SignerInfo": {
                      "SignerType": 2,
                      "ExtendedDocumentTitleType": 10
                    },
                    "MetadataItems": [],
                    "EncryptedMetadataItems": []
                  }
                ],
                "IsActual": true,
                "Workflows": [
                  {
                    "Id": 3,
                    "IsDefault": true
                  }
                ]
              }
            ]
          }
        ]
      }

- ``documentTypeNamedId`` = ``Torg2`` — имя типа документа,
- ``documentFunction`` = ``NoAdditionalInfo`` — функция для однотитульного документа, ``WithAdditionalInfo`` — функция для двухтитульного,
- ``documentVersion`` = ``torg2_05_01_01`` — версия формата,
- ``titleIndex`` = ``0`` — титул покупателя,
- ``UserDataXsdUrl`` —  URL-путь метода, возвращающего файл XSD-схемы контракта для генерации титула с помощью метода генерации.

Отправка файла титула покупателя для акта об установленном расхождении ТОРГ-2
-----------------------------------------------------------------------------

Титул покупателя можно отправить с помощью метода :doc:`../http/PostMessage`. 

Для этого подготовьте структуру :doc:`../proto/MessageToPost`:

- в поле ``FromBoxId`` укажите идентификатор ящика отправителя;
- в поле ``ToBoxId`` укажите идентификатор ящика получателя;
- для передачи XML-файла титула покупателя акта ТОРГ-2 используйте вложенную структуру ``DocumentAttachment``:

	- XML-файл передайте в структуре ``SignedContent`` в поле ``Content``, подпись — в поле ``Signature``;
	- ``TypeNamedId=Torg2``;
	- поле ``Function`` зависит от элемента ``ИнфДопСв``:

		- Если ``ИнфДопСв=1``, укажите значение ``Function=NoAdditionalInfo``,
		- Если ``ИнфДопСв`` принимает другое значение, укажите ``Function=WithAdditionalInfo``.
	
	- ``Version=torg2_05_01_01``.

Описание структур, используемых при отправке ТОРГ-2:

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

Пример тела запроса:

::

    "FromBoxId": "db32772b-9256-49a8-a133-fda593fda38a",
    "ToBoxId": "13254c42-b4f7-4fd3-3324-0094aeb0f15a",
    "DocumentAttachments": [
            {
                "SignedContent":
                {
                    "Content": "PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0...NC50Ls+",        //контент xml-файла в кодировке base-64
                    "Signature": "MIIN5QYJKoZIhvcNAQcCoIIN1jCCDdIA...kA9MJfsplqgW",       //контент файла подписи в кодировке base-64
                },
                "TypeNamedId": "Torg2",
                "Function": "WithAdditionalInfo",
                "Version": "torg2_05_01_01"
            }
        ]
    }

После отправки в теле ответа будет содержаться отправленное сообщение, сериализованное в протобуфер :doc:`../proto/Message`.

Все дальнейшие действия происходят на стороне продавца.

Поиск и получение акта об установленном расхождении ТОРГ-2
----------------------------------------------------------

Чтобы найти все входящие акты ТОРГ-2, которые нужно обработать, используйте метод :doc:`../http/GetDocuments`:

- в поле ``boxId`` укажите идентификатор ящика, в котором нужно найти входящие документы;
- в поле ``filterCategory`` укажите статус и тип документа: ``Torg2.InboundNotFinished``.

Пример запроса на получение акта ТОРГ-2:

::

    GET /V3/GetDocuments?filterCategory=XmlTorg2.InboundNotFinished&boxId=db32772b-9256-49a8-a133-fda593fda38a HTTP/1.1
    Host: diadoc-api.kontur.ru
    Accept: application/json
    Content-Type: application/json charset=utf-8
    Authorization: DiadocAuth ddauth_api_client_id={{ключ разработчика}}, ddauth_token={{авторизационный токен}}

В теле ответа вернется список документов в виде структуры ``DocumentList`` с вложенной структурой ``Document``. Чтобы получить документы, потребуются значения полей ``MessageId`` и ``EntityId``.

Чтобы получить акт об установленном расхождении ТОРГ-2, вызовите метод :doc:`../http/GetMessage` и укажите нужные GET-параметры: ``boxId``, ``messageId``, ``entityId``.

::

    GET /V3/GetMessage?messageId=bbcedb0d-ce34-4e0d-b321-3f600c920935&entityId=30cf2c07-7297-4d48-bc6f-ca7a80e2cf95&boxId=db32772b-9256-49a8-a133-fda593fda38a HTTP/1.1
    Host: diadoc-api.kontur.ru
    Accept: application/json
    Content-Type: application/json charset=utf-8
    Authorization: DiadocAuth ddauth_api_client_id={{ключ разработчика}}, ddauth_token={{авторизационный токен}}

Формирование файла титула доп. сведений для акта об установленном расхождении ТОРГ-2
------------------------------------------------------------------------------------

Файл титула дополнительных сведений можно сформировать как на стороне интеграционного решения, так и используя метод :doc:`../http/GenerateTitleXml`.

Генерация титула с помощью метода :doc:`../http/GenerateTitleXml` выполняется аналогично титулу покупателя.

Тип и версия файла такие же, как у титула покупателя, отличается номер титула, также возможна только одна функция:

- ``documentTypeNamedId`` = ``Torg2`` — имя типа документа,
- ``documentFunction`` = ``WithAdditionalInfo`` — функция документа,
- ``documentVersion`` = ``torg2_05_01_01`` — версия формата,
- ``titleIndex`` = ``1`` — титул доп. сведений.

Отправка файла титула доп. сведений для акта об установленном расхождении ТОРГ-2
--------------------------------------------------------------------------------

Отправить титул доп. сведений акта ТОРГ-2 можно с помощью метода :doc:`../http/PostMessagePatch`. 

Для этого подготовьте структуру :doc:`../proto/MessagePatchToPost`:

- в поле ``BoxId`` укажите идентификатор ящика, в котором находится исходное сообщение,
- в поле ``MessageId`` укажите идентификатор сообщения, к которому относится дополнение,
- чтобы передать XML-файла титула, используйте структуру ``RecipientTitleAttachment``:

	- ``ParentEntityId`` — идентификатор титула покупателя,
	- XML-файл нужно передать во вложенной структуре ``SignedContent`` в поле ``Content``, подпись — в поле ``Signature``.

Описание структур, используемых при отправке ответного титула ТОРГ-2:

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

Пример тела запроса:

::

    "BoxId": "db32772b-9256-49a8-a133-fda593fda38a",
    "MessageId": "bbcedb0d-ce34-4e0d-b321-3f600c920935",
    "RecipientTitles":
    [
        {
            "ParentEntityId":"30cf2c07-7297-4d48-bc6f-ca7a80e2cf95",
            "SignedContent":
            {
                "Content": "PD94bWwgdmVyc2l...LDQudC7Pg==",        //контент xml-файла в кодировке base-64
                "Signature": "MIIN5QYJKoZIhvc...KsTM6zixgz"        //контент файла подписи в кодировке base-64
            }
        }
    ]
    }

После отправки в теле ответа будет содержаться отправленное дополнение, сериализованное в протобуфер :doc:`../proto/MessagePatch`.