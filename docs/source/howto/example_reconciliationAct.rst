Как отправить и получить акт сверки взаимных расчетов в рекомендованном ФНС формате
===================================================================================

Сценарий работы с актом сверки взаимных расчетов
------------------------------------------------

#. Отправитель формирует файл титула отправителя, подписывает и направляет получателю.

#. Получатель получает файл титула отправителя, подписанный и отправленный отправителем.

#. Получатель формирует файл титула получателя, подписывает своей ЭП и отправляет в ответ к файлу титула отправителя. Через API Диадока можно отправить титул получателя с разногласиями.


Формирование файла титула отправителя для акта сверки взаимных расчетов
-----------------------------------------------------------------------
Cгенерировать файл титула, соответствущий `утвержденному формату <https://normativ.kontur.ru/document?moduleId=1&documentId=425482>`__, можно с помощью метода :doc:`../http/GenerateTitleXml`. Для этого передайте в метод следующие параметры:

		- ``documentTypeNamedId`` — тип документа;
		- ``documentFunction`` — функция документа;
		- ``documentVersion`` — версия документа;
		- ``titleIndex`` — идентификатор титула документа.

В теле запроса нужно передать XML-файл ``UserDataXsd``, соответствующий XSD-схеме. ``UsedDataXsd`` содержит информацию для генерации титула, которую может заполнить только пользователь.

Получить тип, функцию, версию, идентификатор титула и ссылку на скачивание XSD-схемы можно с помощью метода :doc:`../http/GetDocumentTypes`. В ответе метод возвращает описание всех типов документов, доступных в ящике.

Ниже приведено тело ответа метода ``GetDocumentTypes``. Для упрощения из него удалены другие типы, функции, версии и информация о метаданных.

.. container:: toggle

  .. code-block:: protobuf

      {
          "Name": "ReconciliationAct",
          "Title": "Акт сверки",
          "SupportedDocflows": [
              1,
              0
          ],
          "RequiresFnsRegistration": true,
          "Functions": [
              {
                  "Name": "default",
                  "Versions": [
                      {
                      "Version": "reconciliationact405_05_01_01",
                      "SupportsContentPatching": true,
                      "SupportsEncrypting": false,
                      "SupportsPredefinedRecipientTitle": false,
                      "SupportsAmendmentRequest": true,
                      "Titles": [
                          {
                          "Index": 0,
                          "IsFormal": true,
                          "XsdUrl": "/GetContent?typeNamedId=ReconciliationAct&function=default&version=reconciliationact405_05_01_01&titleIndex=0&contentType=TitleXsd",
                          "UserDataXsdUrl": "/GetContent?typeNamedId=ReconciliationAct&function=default&version=reconciliationact405_05_01_01&titleIndex=0&contentType=UserContractXsd",
                          "SignerInfo": {
                          "SignerType": 3,
                          "ExtendedDocumentTitleType": -1,
                          "SignerUserDataXsdUrl": "/GetContent?typeNamedId=ReconciliationAct&function=default&version=reconciliationact405_05_01_01&titleIndex=0&contentType=SignerUserContractXsd"
                          },
                          "MetadataItems": [],
                          "EncryptedMetadataItems": []
                          },
                          {
                          "Index": 1,
                          "IsFormal": true,
                          "XsdUrl": "/GetContent?typeNamedId=ReconciliationAct&function=default&version=reconciliationact405_05_01_01&titleIndex=1&contentType=TitleXsd",
                          "UserDataXsdUrl": "/GetContent?typeNamedId=ReconciliationAct&function=default&version=reconciliationact405_05_01_01&titleIndex=1&contentType=UserContractXsd",
                          "SignerInfo": {
                              "SignerType": 3,
                              "ExtendedDocumentTitleType": -1,
                              "SignerUserDataXsdUrl": "/GetContent?typeNamedId=ReconciliationAct&function=default&version=reconciliationact405_05_01_01&titleIndex=1&contentType=SignerUserContractXsd"
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

- ``documentTypeNamedId`` = ``ReconciliationAct`` — имя типа документа,
- ``documentFunction`` = ``default`` — функция документа,
- ``documentVersion`` = ``reconciliationact405_05_01_01`` — версия формата,
- ``titleIndex`` = ``0`` — титул отправителя,
- ``UserDataXsdUrl`` —  URL-путь метода, возвращающего файл XSD-схемы контракта для генерации титула с помощью метода генерации.

Отправка файла титула отправителя для акта сверки взаимных расчетов
-------------------------------------------------------------------

Полученный XML-файл титула отправителя можно отправить с помощью метода :doc:`../http/PostMessage`. 

В теле запроса метода передайте структуру :doc:`../proto/MessageToPost`, заполненную следующими данными:

- в поле ``FromBoxId`` укажите идентификатор ящика отправителя;
- в поле ``ToBoxId`` укажите идентификатор ящика получателя;
- для передачи XML-файла титула отправителя акта сверки используйте вложенную структуру ``DocumentAttachment``:

	- XML-файл передайте в поле ``Content`` структуры ``SignedContent``, подпись — в поле ``Signature``;
	- ``TypeNamedId=ReconciliationAct``;
	- ``Function=default``;
	- ``Version=reconciliationact405_05_01_01``.

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
                "TypeNamedId": "ReconciliationAct",
                "Function": "default",
                "Version": "reconciliationact405_05_01_01"
            }
        ]
    }

После отправки в теле ответа будет содержаться отправленное сообщение, сериализованное в протобуфер :doc:`../proto/Message`.

Все дальнейшие действия происходят на стороне получателя.

Поиск акта сверки взаимных расчетов
-----------------------------------

Чтобы найти все входящие акты, которые нужно обработать, используйте метод :doc:`../http/GetDocuments`:

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

Получение акта сверки взаимных расчетов
---------------------------------------

Найденный документ можно получить с помощью метода :doc:`../http/GetMessage`. В запросе передайте параметры, вернувшиеся в теле ответа метода ``GetDocuments``: ``boxId``, ``messageId``, ``entityId``.

Пример запроса на получение акта сверки:

::

    GET /V3/GetMessage?messageId=bbcedb0d-ce34-4e0d-b321-3f600c920935&entityId=30cf2c07-7297-4d48-bc6f-ca7a80e2cf95&boxId=db32772b-9256-49a8-a133-fda593fda38a HTTP/1.1
    Host: diadoc-api.kontur.ru
    Accept: application/json
    Content-Type: application/json charset=utf-8
    Authorization: DiadocAuth ddauth_api_client_id={{ключ разработчика}}, ddauth_token={{авторизационный токен}}

Формирование файла титула получателя для акта сверки взаимных расчетов
----------------------------------------------------------------------

Генерация титула получателя с помощью метода :doc:`../http/GenerateTitleXml` выполняется аналогично титулу отправителя.

Тип, функция и версия файла такие же, как у титула отправителя, отличается только номер титула:

- ``documentTypeNamedId`` = ``ReconciliationAct`` — имя типа документа,
- ``documentFunction`` = ``default`` — функция документа,
- ``documentVersion`` = ``reconciliationact405_05_01_01`` — версия формата,
- ``titleIndex`` = ``1`` — титул получателя.

Отправка файла титула получателя для акта сверки взаимных расчетов
------------------------------------------------------------------

Отправить сформированный титул получателя акта сверки можно с помощью метода :doc:`../http/PostMessagePatch`. 

В теле запроса метода передайте структуру :doc:`../proto/MessagePatchToPost`, заполненную следующими данными:

- в поле ``BoxId`` укажите идентификатор ящика, в котором находится исходное сообщение;
- в поле ``MessageId`` укажите идентификатор сообщения, к которому относится дополнение;
- чтобы передать XML-файла титула, используйте структуру ``RecipientTitleAttachment``:

	- ``ParentEntityId`` — идентификатор титула отправителя;
	- XML-файл нужно передать в поле ``Content`` вложенной структуры ``SignedContent``, подпись — в поле ``Signature``.

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