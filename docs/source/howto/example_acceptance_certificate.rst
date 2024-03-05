Как отправить и получить акт о выполнении работ/оказании услуг в рекомендованном ФНС формате
============================================================================================

Сценарий работы с актом о выполнении работ/оказании услуг
---------------------------------------------------------

#. Исполнитель формирует файл титула исполнителя, подписывает и направляет заказчику.

#. Заказчик получает товарную накладную, подписанную и отправленную исполнителем;

#. Заказчик формирует файл титула заказчика, подписывает своей ЭП и отправляет в адрес исполнителя.


.. note:: Более подробно о порядке обмена электронными актами о выполнении работ/оказании услуг между компаниями можно почитать на `сайте <http://www.diadoc.ru/docs/others/acts>`__

Формирование файла титула исполнителя для акта о выполнении работ/оказании услуг
--------------------------------------------------------------------------------

Cгенерировать файл титула, соответствущий утвержденному формату, можно с помощью метода :doc:`../http/GenerateTitleXml`. Для этого передайте в метод следующие параметры:

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
        "Name": "XmlAcceptanceCertificate",
        "Title": "Акт",
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
                "Version": "rezru_05_02_01",
                "SupportsContentPatching": true,
                "SupportsEncrypting": true,
                "SupportsPredefinedRecipientTitle": false,
                "SupportsAmendmentRequest": false,
                "Titles": [
                  {
                    "Index": 0,
                    "IsFormal": true,
                    "XsdUrl": "/GetContent?typeNamedId=XmlAcceptanceCertificate&function=default&version=rezru_05_02_01&titleIndex=0&contentType=TitleXsd",
                    "UserDataXsdUrl": "/GetContent?typeNamedId=XmlAcceptanceCertificate&function=default&version=rezru_05_02_01&titleIndex=0&contentType=UserContractXsd",
                    "SignerInfo": {
                      "SignerType": 2,
                      "ExtendedDocumentTitleType": 6
                    },
                    "MetadataItems": [],
                    "EncryptedMetadataItems": []
                  },
                  {
                    "Index": 1,
                    "IsFormal": true,
                    "XsdUrl": "/GetContent?typeNamedId=XmlAcceptanceCertificate&function=default&version=rezru_05_02_01&titleIndex=1&  contentType=TitleXsd",
                    "UserDataXsdUrl": "/GetContent?typeNamedId=XmlAcceptanceCertificate&function=default&version=rezru_05_02_01&titleIndex=1&contentType=UserContractXsd",
                    "SignerInfo": {
                      "SignerType": 2,
                      "ExtendedDocumentTitleType": 7
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
                  },
                  {
                    "Id": 9,
                    "IsDefault": false
                  }
                ]
              }
            ]
        ]
      }

- ``documentTypeNamedId`` = ``XmlAcceptanceCertificate`` — имя типа документа,
- ``documentFunction`` = ``default`` — функция документа,
- ``documentVersion`` = ``rezru_05_02_01`` — версия формата,
- ``titleIndex`` = ``0`` — титул исполнителя,
- ``UserDataXsdUrl`` —  URL-путь метода, возвращающего файл XSD-схемы контракта для генерации титула с помощью метода генерации.

Отправка файла титула исполнителя для акта о выполнении работ/оказании услуг
----------------------------------------------------------------------------

Полученный XML-файл титула исполнителя можно отправить с помощью метода :doc:`../http/PostMessage`. 

В теле запроса метода передайте структуру :doc:`../proto/MessageToPost`, заполненную следующими данными:

- в поле ``FromBoxId`` укажите идентификатор ящика отправителя;
- в поле ``ToBoxId`` укажите идентификатор ящика получателя;
- для передачи XML-файла титула отправителя акта сверки используйте вложенную структуру ``DocumentAttachment``:

	- XML-файл передайте в поле ``Content`` структуры ``SignedContent``, подпись — в поле ``Signature``;
	- ``TypeNamedId=XmlAcceptanceCertificate``;
	- ``Function=default``;
	- ``Version=rezru_05_02_01``.

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
                "TypeNamedId": "XmlAcceptanceCertificate",
                "Function": "default",
                "Version": "rezru_05_02_01"
            }
        ]
    }

После отправки в теле ответа будет содержаться отправленное сообщение, сериализованное в протобуфер :doc:`../proto/Message`.

Все дальнейшие действия происходят на стороне заказчика.

Поиск акта о выполнении работ/оказании услуг
--------------------------------------------

Чтобы найти все входящие акты, которые нужно обработать, используйте метод :doc:`../http/GetDocuments`:

- в поле ``boxId`` укажите идентификатор ящика, в котором нужно найти входящие документы;
- в поле ``filterCategory`` укажите статус и тип документа: ``XmlAcceptanceCertificate.InboundNotFinished``.

Пример запроса на поиск акта о выполнении работ/оказании услуг:

::

    GET /V3/GetDocuments?filterCategory=XmlAcceptanceCertificate.InboundNotFinished&boxId=db32772b-9256-49a8-a133-fda593fda38a HTTP/1.1
    Host: diadoc-api.kontur.ru
    Accept: application/json
    Content-Type: application/json charset=utf-8
    Authorization: DiadocAuth ddauth_api_client_id={{ключ разработчика}}, ddauth_token={{авторизационный токен}}

В теле ответа вернется список документов в виде структуры ``DocumentList`` с вложенной структурой ``Document``. Чтобы получить документы, потребуются значения полей ``MessageId`` и ``EntityId``.

Получение акта о выполнении работ/оказании услуг
------------------------------------------------

Найденный документ можно получить с помощью метода :doc:`../http/GetMessage`. В запросе передайте параметры, вернувшиеся в теле ответа метода ``GetDocuments``: ``boxId``, ``messageId``, ``entityId``.

Пример запроса на получение акта о выполнении работ/оказании услуг:

::

    GET /V3/GetMessage?messageId=bbcedb0d-ce34-4e0d-b321-3f600c920935&entityId=30cf2c07-7297-4d48-bc6f-ca7a80e2cf95&boxId=db32772b-9256-49a8-a133-fda593fda38a HTTP/1.1
    Host: diadoc-api.kontur.ru
    Accept: application/json
    Content-Type: application/json charset=utf-8
    Authorization: DiadocAuth ddauth_api_client_id={{ключ разработчика}}, ddauth_token={{авторизационный токен}}

Пример структуры акта о выполнении работ/оказании услуг :doc:`XmlAcceptanceCertificate <../proto/Entity message>` в теле ответа:

.. code-block:: json

   {
       "EntityType": "Attachment",
       "EntityId": "654ac483-0dd4-4085-b70f-565c8b754e10",
       "Content": "lores ipsum",
       "AttachmentType": "XmlAcceptanceCertificate",
       "FileName": "ON_NSCHFDOPPR_2BM-7750370234-4012052808304878702630000000000_2BM_20150927_324c290e-f049-4906-baac-1ddcd7f3c2ff.xml",
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

Формирование файла титула заказчика для акта о выполнении работ/оказании услуг
------------------------------------------------------------------------------

Генерация титула заказчика с помощью метода :doc:`../http/GenerateTitleXml` выполняется аналогично титулу исполнителя.

- ``documentTypeNamedId`` = ``XmlAcceptanceCertificate`` — имя типа документа,
- ``documentFunction`` = ``default`` — функция документа,
- ``documentVersion`` = ``rezru_05_02_01`` — версия формата,
- ``titleIndex`` = ``1`` — титул заказчика.

Отправка файла титула заказчика для акта о выполнении работ/оказании услуг
--------------------------------------------------------------------------
Отправить сформированный титул заказчика акта сверки можно с помощью метода :doc:`../http/PostMessagePatch`. 

В теле запроса метода передайте структуру :doc:`../proto/MessagePatchToPost`, заполненную следующими данными:

- в поле ``BoxId`` укажите идентификатор ящика, в котором находится исходное сообщение;
- в поле ``MessageId`` укажите идентификатор сообщения, к которому относится дополнение;
- чтобы передать XML-файл титула, используйте структуру :ref:`RecipientTitleAttachment`:

	- ``ParentEntityId`` — идентификатор титула исполнителя;
	- XML-файл нужно передать  в поле ``Content`` вложенной структуры ``SignedContent``, подпись — в поле ``Signature``.

Пример тела запроса:

::

    "BoxId": "db32772b-9256-49a8-a133-fda593fda38a",
    "MessageId": "bbcedb0d-ce34-4e0d-b321-3f600c920935",
    "RecipientTitles":
    [
        {
            "ParentEntityId":"30cf2c07-7297-4d48-bc6f-ca7a80e2cf95&",
            "SignedContent":
            {
                "Content": "PD94bWwgdmVyc2l...LDQudC7Pg==",        //контент xml-файла в кодировке base-64
                "Signature": "MIIN5QYJKoZIhvc...KsTM6zixgz"        //контент файла подписи в кодировке base-64
            }
        }
    ]
    }

После отправки в теле ответа будет содержаться отправленное дополнение, сериализованное в протобуфер :doc:`../proto/MessagePatch`.