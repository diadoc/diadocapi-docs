Получение информации о типе документа
=====================================

Каждый документ в Диадоке имеет свой тип. Тип определяет свойства документа, его поведение и требования к содержимому.

Чтобы :doc:`сгенерировать <generation>` формализованный документ с помощью API Диадока, нужно знать следующую информацию о его типе:

	- идентификатор типа документа,
	- функция документа,
	- версия документа,
	- идентификатор титула документа,
	- XSD-схему для формирования XML-файла ``UserDataXml``.

Всю эту информацию можно получить с помощью метода :doc:`../http/GetDocumentTypes`.

В ответе метод ``GetDocumentTypes`` возвращает описание всех типов документов, доступных пользователю в Диадоке. Каждый элемент в списке ответа представлен структурой :doc:`../proto/DocumentTypeDescriptionV2`.

Ниже приведен пример ответа метода ``GetDocumentTypes``. Так как количество типов документов в Диадоке большое, для простоты приведем только часть ответа, описывающую УПД формата 970.

**Пример тела ответа метода GetDocumentTypes:**

.. container:: toggle

 .. code-block:: json

   "Name": "UniversalTransferDocument",
   "Title": "УПД",
   "SupportedDocflows": [ 
     0
   ],
   "RequiresFnsRegistration": true,
   "Functions": [
   {
     "Name": "СЧФ",
     "Versions": [
     {
        "Version": "utd970_05_02_01",
        "SupportsContentPatching": true,
        "SupportsEncrypting": false,
        "SupportsPredefinedRecipientTitle": false,
        "SupportsAmendmentRequest": true,
        "Titles": [
        {
          "Index": 0,
          "IsFormal": true,
          "XsdUrl": "/GetContent?typeNamedId=UniversalTransferDocument&function=СЧФ&version=utd970_05_02_01&titleIndex=0&contentType=TitleXsd",
          "UserDataXsdUrl": "/GetContent?typeNamedId=UniversalTransferDocument&function=СЧФ&version=utd970_05_02_01&titleIndex=0&contentType=UserContractXsd",
          "SignerInfo":
          {
            "SignerType": 3,
            "ExtendedDocumentTitleType": 12,
            "SignerUserDataXsdUrl": "/GetContent?typeNamedId=UniversalTransferDocument&function=СЧФ&version=utd970_05_02_01&titleIndex=0&contentType=SignerUserContractXsd"
          },
          "MetadataItems": [],
          "EncryptedMetadataItems": []
        }
        ],
        "IsActual": true,
        "Workflows": [
        {
          "Id": 17,
          "IsDefault": true
        },
        {
          "Id": 10,
          "IsDefault": false
        }
        ]
     }
     ]
   }
   ]

Из этого ответа можно получить следующие данные:

	- тип документа хранится в поле ``DocumentTypeDescriptionV2.Name``:

	   ``TypeNamedId`` = ``UniversalTransferDocument``,

	- функция документа хранится в поле ``DocumentTypeDescriptionV2.Functions[]``:

	   ``Function`` = ``УПД``,

	- версия документа хранится в поле ``DocumentTypeDescriptionV2.Functions[].Versions[]``:

	   ``Version`` = ``utd970_05_02_01``,

	- идентификатор титула документа хранится в поле ``DocumentTypeDescriptionV2.Functions[].Versions[].Titles[]``:

	   ``IndexTitle`` = ``0`` (титул продавца),

	- ссылка для получения XSD-схемы хранится в поле ``DocumentTypeDescriptionV2.Functions[].Versions[].Titles[].UserDataXsdUrl``:

	   ``UserDataXsdUrl`` = ``/GetContent?typeNamedId=UniversalTransferDocument&function=СЧФ&version=utd970_05_02_01&titleIndex=0&contentType=UserContractXsd``.

Чтобы получить XSD-схему для формирования ``UserDataXml``, вызовите метод по ссылке из поля ``UserDataXsdUrl``.

Полученные значения можно использовать для :doc:`генерации формализованного документа<generation>`.