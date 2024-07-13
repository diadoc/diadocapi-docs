Получение информации о типе документа
=====================================

.. contents:: :local:
	:depth: 3

Каждый документ в Диадоке имеет свой тип. Тип определяет свойства документа, его поведение и требования к содержимому.


.. _doctype_getdata:

Получение данных о типе документа
---------------------------------

Чтобы получить данные о типе документа:

	#. Вызовите метод :doc:`../http/GetDocumentTypes`. В ответе метод возвращает описание всех типов документов, доступных пользователю в Диадоке в указанном ящике. Каждый элемент в списке ответа представлен структурой :doc:`../proto/DocumentTypeDescriptionV2`.
	#. Среди полученного списка найдите описание типа, который требуется для вашего интеграционного решения.

Ниже приведен пример ответа метода ``GetDocumentTypes``. Так как количество типов документов в Диадоке большое, для простоты приведем только часть ответа, описывающую УПД формата 970 с функцией СЧФ.

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


.. _doctype_title:

Данные для генерации титула
---------------------------

Чтобы :doc:`сгенерировать <generation>` формализованный документ с помощью API Диадока, нужно знать следующую информацию о его типе:

	- идентификатор типа документа,
	- функция документа,
	- версия документа,
	- идентификатор титула документа,
	- XSD-схема для формирования упрощенного XML-файла UserDataXml.

Из :ref:`полученного выше <doctype_getdata>` ответа метода ``GetDocumentTypes`` получаем следующие данные:

	- ``DocumentTypeDescriptionV2.Name`` — тип документа: ``UniversalTransferDocument``,
	- ``DocumentTypeDescriptionV2.Functions[].Name`` — функция документа: ``СЧФ``,
	- ``DocumentTypeDescriptionV2.Functions[].Versions[].Version`` — версия документа: ``utd970_05_02_01``,
	- ``DocumentTypeDescriptionV2.Functions[].Versions[].Titles[].Index`` — идентификатор титула документа: ``0`` (титул продавца),
	- ``DocumentTypeDescriptionV2.Functions[].Versions[].Titles[].UserDataXsdUrl`` — ссылка для получения XSD-схемы упрощенного XML-файла титула: ``/GetContent?typeNamedId=UniversalTransferDocument&function=СЧФ&version=utd970_05_02_01&titleIndex=0&contentType=UserContractXsd``.

Чтобы получить упрощенную XSD-схему для формирования UserDataXml, вызовите метод ``GetContent`` по ссылке из поля ``UserDataXsdUrl``. Ссылка для получения полной XSD-схемы титула хранится в поле ``XsdUrl``.

Полученные значения можно использовать для :doc:`генерации формализованного документа<generation>`.


.. _doctype_signer:

Данные для формирования подписанта
----------------------------------

Описание типа документа содержит информацию о подписанте для каждого титула формализованного документа. Эта информация хранится в структуре :ref:`signer-info2`.

Из :ref:`полученного выше <doctype_getdata>` ответа метода ``GetDocumentTypes`` получаем следующие данные:

	- ``DocumentTypeDescriptionV2.Functions[].Versions[].Titles[].SignerInfo.SignerType`` — тип подписанта: ``3`` — универсальный подписант,
	- ``DocumentTypeDescriptionV2.Functions[].Versions[].Titles[].SignerInfo.ExtendedDocumentTitleType`` — тип титула документа: ``12`` — данные для титула покупателя УПД формата 970,
	- ``DocumentTypeDescriptionV2.Functions[].Versions[].Titles[].SignerInfo.SignerUserDataXsdUrl`` — ссылка для получения XSD-схемы упрощенного XML-фала универсального подписанта: "/GetContent?typeNamedId=UniversalTransferDocument&function=СЧФ&version=utd970_05_02_01&titleIndex=0&contentType=SignerUserContractXsd"

Чтобы получить упрощенную XSD-схему для формирования XML-блока универсального подписанта, вызовите метод ``GetContent`` по ссылке из поля ``SignerUserDataXsdUrl``. В ответ метод вернет файл XSD-схемы SignerUserData.xsd.

Полученные значения можно использовать для :doc:`генерации блока подписанта <preparetosign>`.


----

.. rubric:: См. также

*Инструкции:*
	- :doc:`generation`
	- :doc:`preparetosign`

*Методы для работы с типами документов:*
	- :doc:`../http/GetDocumentTypes` — возвращает описание типов документов