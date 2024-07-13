Работа с УПД в 820 и 970 форматах
=================================

.. contents:: :local:
	:depth: 3

До 1 апреля 2025 года можно использовать следующие форматы универсального передаточного документа (УПД):

	- Формат №820, утвержденный `приказом ФНС России от 19.12.2018 № ММВ-7-15/820@ <https://normativ.kontur.ru/document?moduleId=1&documentId=328588>`_,
	- Формат №970, утвержденный `приказом ФНС России от 19.12.2023 № ЕД-7-26/970@ <https://normativ.kontur.ru/document?moduleId=1&documentId=464695>`_.

**После 1 апреля 2025 года можно будет использовать только формат №970.**

Эти форматы распространяются на следующие типы документов:

	- счет-фактуру;
	- первичный документ, подтверждающий совершение хозяйственной операции — накладные, акты и другие первичные документы;
	- универсальный передаточный документ (УПД), который совмещает в себе счет-фактуру и первичный документ, подтверждающий совершение хозяйственной операции.

Форма универсального передаточного документа и рекомендации по его заполнению приведены в письме ФНС России `от 21.10.13 № ММВ-20-3/96@ <https://normativ.kontur.ru/document?moduleId=1&documentId=220334>`__.

.. note::
	Методы и подходы, описанные ниже, можно использовать для работы с УПД, накладными, актами и счетами-фактурами.

Сценарий работы с УПД включает следующие шаги:

	- Продавец:
		- генерирует титул продавца,
		- отправляет его покупателю.
	- Покупатель:
		- получает титул продавца,
		- при необходимости парсит полученный титул, 
		- генерирует титул покупателя,
		- отправляет его продавцу.


Генерация титула продавца
-------------------------

Для генерации титула продавца используйте метод :doc:`../http/GenerateTitleXml`. Инструкция о генерации приведена на странице :doc:`../instructions/generation`.

Чтобы сгенерировать титул продавца, нужно получить необходимую информацию из метода :doc:`../http/GetDocumentTypes`. Инструкция о получении данных для титула из метода ``GetDocumentTypes`` приведена в разделе :ref:`doctype_title`.

Из ответа метода ``GetDocumentTypes`` для УПД возьмем следующие значения для параметров метода ``GenerateTitleXml``:

.. tabs::

	.. tab:: УПД 970

		- ``documentTypeNamedId = UniversalTransferDocument``,
		- ``documentFunction = СЧФДОП``,
		- ``documentVersion = utd970_05_02_01``,
		- ``titleIndex = 0`` (титул продавца).

	.. tab:: УПД 820

		- ``documentTypeNamedId = UniversalTransferDocument``,
		- ``documentFunction = СЧФДОП``,
		- ``documentVersion = utd820_05_01_02_hyphen``,
		- ``titleIndex = 0`` (титул продавца).

Кроме этого нужно подготовить содержимое титула — упрощенный XML-файл UserDataXml. Подробнее см. :doc:`../instructions/generation`.

С помощью полученных данных можно сгенерировать титул продавца методом :doc:`../http/GenerateTitleXml`.

**Пример HTTP-запроса метода GenerateTitleXml:**

.. tabs::

	.. tab:: УПД 970

		.. code-block:: http

			POST /GenerateTitleXml?boxId={{boxId_sender}}&documentTypeNamedId=UniversalTransferDocument&documentFunction=СЧФДОП&documentVersion=utd970_05_02_01&titleIndex=0 HTTP/1.1
			Host: diadoc-api.kontur.ru
			Authorization: DiadocAuth ddauth_api_client_id={{apiKey}}, ddauth_token={{token}}
			Content-Type: application/xml; charset=utf-8

	.. tab:: УПД 820

		.. code-block:: http

			POST /GenerateTitleXml?boxId={{boxId_sender}}&documentTypeNamedId=UniversalTransferDocument&documentFunction=СЧФДОП&documentVersion=utd820_05_01_02_hyphen&titleIndex=0 HTTP/1.1
			Host: diadoc-api.kontur.ru
			Authorization: DiadocAuth ddauth_api_client_id={{apiKey}}, ddauth_token={{token}}
			Content-Type: application/xml; charset=utf-8

**Пример тела запроса метода GenerateTitleXml (UserDataXml):**

.. tabs::

	.. tab:: УПД 970

		.. container:: toggle

			.. literalinclude:: ../inline/utd970_05_02_01_title0_body.xml

	.. tab:: УПД 820

		.. container:: toggle

			.. literalinclude:: ../inline/utd820_05_01_02_hyphen_title0_body.xml

**Пример тела ответа метода GenerateTitleXml (титул продавца):**

.. tabs::

	.. tab:: УПД 970

		.. container:: toggle

			.. literalinclude:: ../inline/utd970_05_02_01_title0_resp.xml
				:encoding: windows-1251

	.. tab:: УПД 820

		.. container:: toggle

			.. literalinclude:: ../inline/utd820_05_01_02_hyphen_title0_resp.xml
				:encoding: windows-1251


Отправка титула продавца
------------------------

Сформированный титул продавца можно подписать и отправить покупателю с помощью метода :doc:`../http/PostMessage`. Инструкция об отправке документа приведена в разделе :ref:`doc_send`.

**Пример тела запроса метода PostMessage:**

.. tabs::

	.. tab:: УПД 970

		.. container:: toggle

		 .. code-block:: json

			"FromBoxId": "db32772b-9256-49a8-a133-fda593fda38a",
			"ToBoxId": "13254c42-b4f7-4fd3-3324-0094aeb0f15a",
			"DocumentAttachments": [
				{
					"SignedContent":
					{
						"Content": "PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0...NC50Ls+",		// содержимое XML-файла в кодировке base-64
						"Signature": "MIIN5QYJKoZIhvcNAQcCoIIN1jCCDdIA...kA9MJfsplqgW",		// содержимое файла подписи в кодировке base-64
					},
					"TypeNamedId": "UniversalTransferDocument",
					"Function": "СЧФ",
					"Version": "utd970_05_02_01"
				}
			]

	.. tab:: УПД 820

		.. container:: toggle

		 .. code-block:: json

			"FromBoxId": "a96be310-0982-461a-8b2a-91d198b7861c",
			"ToBoxId": "13254c42-b4f7-4fd3-3324-0094aeb0f15a",
			"DocumentAttachments": [
				{
					"SignedContent":
					{
						"Content": "PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0...NC50Ls+",		// содержимое XML-файла в кодировке base-64
						"Signature": "MIIN5QYJKoZIhvcNAQcCoIIN1jCCDdIA...kA9MJfsplqgW",		// содержимое файла подписи в кодировке base-64
					},
					"TypeNamedId": "UniversalTransferDocument",
					"Function": "СЧФДОП",
					"Version": "utd820_05_01_02_hyphen"
				}
			]

После отправки титула продавца Диадок автоматически формирует подтверждение оператора о дате получения документа, а покупатель формирует извещение о получении титула и отправляет его продавцу. О том, как получить эти служебные документы, написано в инструкциях:

	- :ref:`service_get_InvoiceConfirmation`
	- :ref:`service_get_InvoiceReceipt`


Получение титула продавца в ящике покупателя
--------------------------------------------

Получение через ленту событий
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

О появлении титула продавца в ящике покупателя можно узнать с помощью методов чтения ленты событий: :doc:`../http/GetNewEvents` и :doc:`../http/GetDocflowEvents_V3`.

Отличить формат полученного документа можно по ответам этих методов. В них возвращается версия документа ``Version``:

	- для документов 820 формата версия будет начинаться с ``utd820``, — например, ``utd820_05_01_02_hyphen``,
	- для документов 970 формата версия будет иметь значение ``utd970_05_02_01``.

Из ленты событий можно узнать идентификаторы документа ``MessageId`` и ``DocumentId``, а также запросить дополнительную информацию по документу с помощью методов :doc:`../http/GetMessage`, :doc:`../http/GetDocument`, :doc:`../http/GetDocflows_V3`.

Получение через поиск
~~~~~~~~~~~~~~~~~~~~~

Чтобы найти все входящие документы, которые нужно обработать, используйте метод :doc:`../http/GetDocuments`:

	- в поле ``boxId`` укажите идентификатор ящика, в котором нужно найти входящие документы;
	- в поле ``filterCategory`` укажите статус и тип документа ``UniversalTransferDocument.InboundNotFinished``.

HTTP-запрос на поиск УПД будет выглядеть следующим образом:

**Пример HTTP-запроса метода GetDocuments:**

.. code-block:: http

	GET /V3/GetDocuments?filterCategory=UniversalTransferDocument.InboundNotFinished&boxId=db32772b-9256-49a8-a133-fda593fda38a HTTP/1.1
	Host: diadoc-api.kontur.ru
	Accept: application/json
	Content-Type: application/json charset=utf-8
	Authorization: DiadocAuth ddauth_api_client_id={{ключ разработчика}}, ddauth_token={{авторизационный токен}}

В теле ответа вернется список документов в виде структуры :doc:`../proto/DocumentList` с вложенной структурой :doc:`../proto/Document`. Отличить формат документа можно по значению поля ``Version``:

	- для документов 820 формата версия будет начинаться с ``utd820``, — например, ``utd820_05_01_02_hyphen``,
	- для документов 970 формата версия будет иметь значение ``utd970_05_02_01``.

Найденный документ можно получить с помощью метода :doc:`../http/GetMessage`. В запросе передайте параметры, вернувшиеся в теле ответа метода ``GetDocuments``: ``boxId``, ``messageId``, ``entityId``.

HTTP-запрос на получение УПД будет выглядеть следующим образом:

**Пример HTTP-запроса метода GetMessage:**

.. code-block:: http

	GET /V3/GetMessage?messageId=bbcedb0d-ce34-4e0d-b321-3f600c920935&entityId=30cf2c07-7297-4d48-bc6f-ca7a80e2cf95&boxId=db32772b-9256-49a8-a133-fda593fda38a HTTP/1.1
	Host: diadoc-api.kontur.ru
	Accept: application/json
	Content-Type: application/json charset=utf-8
	Authorization: DiadocAuth ddauth_api_client_id={{ключ разработчика}}, ddauth_token={{авторизационный токен}}

После получения титула продавца нужно :ref:`сформировать и отправить извещение о получении <service_send_InvoiceReceipt>`.


Парсинг титула продавца
-----------------------

Получить данные о полученном титуле продавца можно следующими способами:

	- взять данные сразу из структуры полученного титула,
	- выполнить парсинг документа, чтобы работать с упрощенным XML-файлом UserDataXml.

Выполнить парсинг документа можно с помощью метода :doc:`../http/ParseTitleXml`.
Для этого необходимо знать тип документа, функцию, версию и номер титула.
Узнать тип, функцию и версию можно следующими способами:

	- из ответов методов :doc:`../http/GetNewEvents`, :doc:`../http/GetDocflowEvents_V3`,  :doc:`../http/GetDocflows_V3`, :doc:`../http/GetMessage`, :doc:`../http/GetDocument`,
	- с помощью метода детектирования :doc:`../http/DetectDocumentTitles`.

**Пример HTTP-запроса метода ParseTitleXml:**

.. code-block:: http

	POST /ParseTitleXml?boxId=13254c42-b4f7-4fd3-3324-0094aeb0f15a&documentTypeNamedId=UniversalTransferDocument&documentFunction=СЧФДОП&documentVersion=utd820_05_01_02_hyphen&titleIndex=0 HTTP/1.1
		Host: diadoc-api.kontur.ru
		Authorization: DiadocAuth ddauth_api_client_id={{ключ разработчика}}, ddauth_token={{авторизационный токен}}
		Content-Type: application/xml; charset=utf-8

В теле запроса нужно передать XML-файл полученного титула.

В ответе метод вернет упрощенный XML-файл UserDataXml, аналогичный тому, который был использован при генерации. Не всегда полученный упрощенный XML-файл ответа метода парсинга будет совпадать с упрощенным XML-файлом запроса метода генерации. Это связано с тем, что при генерации документа Диадок автоматически заполняет данные в титуле. Например, по идентификатору ящика Диадок определяет его реквизиты - ИНН, КПП, наименование и т.д. и добавляет их в XML-файл. Поэтому после парсинга в XML-файле будут указаны ИНН, КПП и наименование организации, а не идентификатор ящика, указанный при генерации.

После получения упрощенного XML-файла пользователь может использовать его в своем интеграционном решении.


Генерация титула покупателя
---------------------------

Титул покупателя генерируется аналогично титулу продавца. 

Для генерации титула покупателя используйте метод :doc:`../http/GenerateTitleXml`. Инструкция о генерации приведена на странице :doc:`../instructions/generation`.

Чтобы сгенерировать титул покупателя, нужно получить необходимую информацию из метода :doc:`../http/GetDocumentTypes`. Инструкция о получении данных для титула из метода ``GetDocumentTypes`` приведена в разделе :ref:`doctype_title`.

Из ответа метода ``GetDocumentTypes`` для УПД в 820 формате возьмем те же значения для параметров метода ``GenerateTitleXml``, что и для титула продавца, но номер титула будет другой:

.. tabs::

	.. tab:: УПД 970

		- ``documentTypeNamedId`` = ``UniversalTransferDocument``,
		- ``documentFunction`` = ``СЧФ``,
		- ``documentVersion`` = ``utd970_05_02_01``,
		- ``titleIndex`` = ``1`` (титул покупателя).

	.. tab:: УПД 820

		- ``documentTypeNamedId`` = ``UniversalTransferDocument``,
		- ``documentFunction`` = ``СЧФДОП``,
		- ``documentVersion`` = ``utd820_05_01_02_hyphen``,
		- ``titleIndex`` = ``1`` (титул покупателя).

Кроме этого нужно подготовить содержимое титула — упрощенный XML-файл UserDataXml. Подробнее см. :doc:`../instructions/generation`.

С помощью полученных данных можно сгенерировать титул покупателя методом :doc:`../http/GenerateTitleXml`.

**Пример HTTP-запроса метода GenerateTitleXml:**

.. tabs::

	.. tab:: УПД 820

		.. code-block:: http

			POST /GenerateTitleXml?boxId=13254c42-b4f7-4fd3-3324-0094aeb0f15&documentTypeNamedId=UniversalTransferDocument&documentFunction=СЧФДОП&documentVersion=utd820_05_01_02_hyphen&titleIndex=1&letterId=93bdfb88-7b80-484d-883d-765102ca5af5&documentId=fc3c3811-3368-4e47-95f4-5334b9a42654 HTTP/1.1
			Host: diadoc-api.kontur.ru
			Authorization: DiadocAuth ddauth_api_client_id={{ключ разработчика}}, ddauth_token={{авторизационный токен}}
			Content-Type: application/xml; charset=utf-8

**Пример тела запроса метода GenerateTitleXml (UserDataXml):**

.. tabs::

	.. tab:: УПД 820

		.. container:: toggle

		 .. code-block:: xml

			<?xml version="1.0" encoding="utf-8"?>
			<UniversalTransferDocumentBuyerTitle DocumentCreator="ИП Покупатель Иван Иванович" OperationContent="Принято без претензий" xmlns:xs="http://www.w3.org/2001/XMLSchema">
				<Signers>
					<SignerDetails LastName="Покупатель" 
						FirstName="Иван" 
						MiddleName="Иванович" 
						SignerPowers="1" 
						SignerPowersBase="Должностные обязанности" 
						SignerStatus="5" 
						SignerType="2" 
						Inn="114500647890" />
				</Signers>
			</UniversalTransferDocumentBuyerTitle>

**Пример тела ответа метода GenerateTitleXml (титул покупателя):**

.. tabs::

	.. tab:: УПД 820

		.. code-block:: xml

			HTTP/1.1 200 OK

			<?xml version="1.0" encoding="windows-1251"?>
			<Файл ИдФайл="ON_NSCHFDOPPOK_2BM-participantId1_2BM-participantid2_f3caa5ab-5033-431f-ba0d-3312ee82b25b" ВерсФорм="5.01" ВерсПрог="Diadoc 1.0">
				<СвУчДокОбор ИдОтпр="2BM-7750370234-4012052808304878702630000000000" ИдПол="2BM-7750370234-4012052808304878702630000000004">
					<СвОЭДОтпр ИННЮЛ="6663003127" ИдЭДО="2BM" НаимОрг="АО &quot;ПФ &quot;СКБ Контур&quot;" />
				</СвУчДокОбор>
				<ИнфПок КНД="1115132" ВремИнфПок="14.50.14" ДатаИнфПок="17.10.2019" НаимЭконСубСост="ИП Покупатель Иван Иванович">
					<ИдИнфПрод ВремФайлИнфПр="14.32.21" ДатаФайлИнфПр="20.05.2019" ИдФайлИнфПр="ON_NSCHFDOPPR_2BM-participantId2_2BM-participantId1_20191011_2ebfc880-6e31-4042-8302-c5201523fc3c">
						<ЭП>MIAGCSqGSIb3DQEHAq...agAAAAAAAA==</ЭП>
					</ИдИнфПрод>
					<СодФХЖ4 ДатаСчФИнфПр="01.02.2003" НаимДокОпрПр="Счет-фактура и документ об отгрузке товаров (выполнении работ), передаче имущественных прав (документ об оказании услуг)" Функция="СЧФДОП" НомСчФИнфПр="140">
						<СвПрин СодОпер="Принято без претензий" />
					</СодФХЖ4>
					<Подписант ОснПолн="Должностные обязанности" ОблПолн="1" Статус="5">
						<ИП ИННФЛ="114500647890">
						<ФИО Фамилия="Покупатель" Имя="Иван" Отчество="Иванович" />
						</ИП>
					</Подписант>
				</ИнфПок>
			</Файл>


Отправка титула покупателя
--------------------------

Сформированный титул покупателя можно подписать и отправить продавцу с помощью метода :doc:`../http/PostMessagePatch`. Инструкция об отправке дополнения приведена в разделе :ref:`doc_patch`.

В результате этих действий получается УПД с двумя подписанными титулами.


XSD-схемы и UserDataXsd
-----------------------

Актуальные XSD-схемы и UserDataXml можно получить с помощью метода :doc:`../http/GetDocumentTypes`. Инструкция о получении данных для титула из метода ``GetDocumentTypes`` приведена в разделе :ref:`doctype_title`.

.. table:: XSD-схемы для соответствующих версий УПД

	+-------------+------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------+
	| Формат      | Версия                 | Титул продавца (titleIndex = 0)                                                                                                                    | Титул покупателя (titleIndex = 1)                                                                                                             |
	|             |                        +------------------------------------------------------------------+---------------------------------------------------------------------------------+-------------------------------------------------------------------+---------------------------------------------------------------------------+
	|             |                        | XSD-схема                                                        | UserDataXsd                                                                     | XSD-схема                                                         | UserDataXsd                                                               |
	+=============+========================+==================================================================+=================================================================================+===================================================================+===========================================================================+
	| Приказ №970 | utd970_05_02_01        | :download:`скачать <../xsd/ON_NSCHFDOPPR_1_997_01_05_02_01.xsd>` | :download:`скачать <../xsd/ON_NSCHFDOPPR_UserContract_970_05_02_01.xsd>`        | :download:`скачать <../xsd/ON_NSCHFDOPPOK_1_997_02_05_02_01.xsd>` | :download:`скачать <../xsd/ON_NSCHFDOPPOK_UserContract_970_05_02_01.xsd>` |
	+-------------+------------------------+------------------------------------------------------------------+---------------------------------------------------------------------------------+-------------------------------------------------------------------+---------------------------------------------------------------------------+
	| Приказ №820 | utd820_05_01_02_hyphen | :download:`скачать <../xsd/ON_NSCHFDOPPR_1_997_01_05_01_03.xsd>` | :download:`скачать <../xsd/ON_NSCHFDOPPR_UserContract_820_05_01_02_Hyphen.xsd>` | :download:`скачать <../xsd/ON_NSCHFDOPPOK_1_997_02_05_01_02.xsd>` | :download:`скачать <../xsd/ON_NSCHFDOPPOK_UserContract_820_05_01_02.xsd>` |
	|             +------------------------+------------------------------------------------------------------+---------------------------------------------------------------------------------+-------------------------------------------------------------------+---------------------------------------------------------------------------+
	|             | utd820_05_01_01_hyphen | :download:`скачать <../xsd/ON_NSCHFDOPPR_1_997_01_05_01_01.xsd>` | :download:`скачать <../xsd/ON_NSCHFDOPPR_UserContract_820_05_01_01_Hyphen.xsd>` | :download:`скачать <../xsd/ON_NSCHFDOPPOK_1_997_02_05_01_01.xsd>` | :download:`скачать <../xsd/ON_NSCHFDOPPOK_UserContract_820_05_01_01.xsd>` |
	+-------------+------------------------+------------------------------------------------------------------+---------------------------------------------------------------------------------+-------------------------------------------------------------------+---------------------------------------------------------------------------+




----

.. rubric:: См. также

*Инструкции:*
	- :doc:`getdoctypes`
	- :doc:`generation`