GenerateTitleXml
================

.. contents:: :local:

Метод ``GenerateTitleXml`` генерирует XML-файл любого титула для любого типа документа. 

.. http:post:: /GenerateTitleXml

	:queryparam boxId: идентификатор ящика
	:queryparam documentTypeNamedId: уникальный строковый идентификатор типа документа
	:queryparam documentFunction: строковый идентификатор функции, уникальный в рамках типа документа
	:queryparam documentVersion: строковый идентификатор версии, уникальный в рамках функции типа документа
	:queryparam titleIndex: числовой идентификатор титула документа
	:queryparam disableValidation: отключение валидации полученного XML-документа по XSD-схеме данного типа документа, необязательный параметр
	:queryparam editingSettingId: идентификатор настройки редактирования содержимого документа, необязательный параметр
	:queryparam letterId: идентификатор сообщения, содержащего соответствующий титул отправителя; параметр обязателен при генерации титула получателя (``titleIndex`` > 0), необязательный в остальных случаях
	:queryparam documentId: идентификатор документа, содержащего соответствующий титул отправителя; параметр обязателен при генерации титула получателя (``titleIndex`` > 0), необязательный в остальных случаях

	:requestheader Authorization: данные, необходимые для :doc:`авторизации <../Authorization>`

	:request Body: Тело запроса должно содержать упрощенный XML-файл ``UserDataXsd``, соответствующий XSD-схеме контракта для генерации титула. XSD-схему контракта можно получить с помощью ссылки из поля ``UserDataXsdUrl`` контракта :ref:`DocumentTitle <document_title>`, полученного методом :doc:`GetDocumentTypes`.

	:resheader Content-Disposition: имя файла сгенерированного титула
	
	:response Body: Тело ответа содержит сгенерированный XML-файл титула, построенный на основании данных из запроса в соответствии с XSD-схемой.
	
	:statuscode 200: операция успешно завершена
	:statuscode 400: данные в запросе имеют неверный формат или отсутствуют обязательные параметры
	:statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization`` или в этом заголовке содержатся некорректные авторизационные данные
	:statuscode 402: закончилась подписка на API
	:statuscode 403: у пользователя нет права для работы с указанным типом документа
	:statuscode 405: используется неподходящий HTTP-метод
	:statuscode 500: при обработке запроса возникла непредвиденная ошибка

Генерация титула отправителя
----------------------------

Пример генерации счета-фактуры формата приказа ФНС №820.

1. Найдем нужный тип и версию документа с помощью метода :doc:`GetDocumentTypes`.

 Ниже приведено тело ответа метода ``GetDocumentTypes``. Для упрощения из него удалены другие типы, функции, версии и информация о метаданных.

.. sourcecode:: js 

    "DocumentTypes": [
        {
            "Name": "Invoice",
            "Title": "Счет-фактура",
            "SupportedDocflows": [
                0
            ],
            "RequiresFnsRegistration": true,
            "Functions": [
                {
                    "Name": "default",
                    "Versions": [
                        {
                            "Version": "utd820_05_01_02_hyphen",
                            "SupportsContentPatching": true,
                            "SupportsEncrypting": true,
                            "SupportsPredefinedRecipientTitle": false,
                            "SupportsAmendmentRequest": true,
                            "Titles": [
                                {
                                    "Index": 0,
                                    "IsFormal": true,
                                    "XsdUrl": "/GetContent?typeNamedId=Invoice&function=default&version=utd820_05_01_02_hyphen&titleIndex=0&contentType=TitleXsd",
                                    "UserDataXsdUrl": "/GetContent?typeNamedId=Invoice&function=default&version=utd820_05_01_02_hyphen&titleIndex=0&contentType=UserContractXsd",
                                    "SignerInfo": {
                                        "SignerType": 2,
                                        "ExtendedDocumentTitleType": 0
                                    },
                                    "MetadataItems": [...],
                                    "EncryptedMetadataItems": [...]
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
        }
    ]
	
Из полученной информации важны следующие значения:

 - ``documentTypeNamedId`` = ``Invoice`` — имя типа документа
 - ``documentFunction`` = ``default`` — функция документа, у счета-фактуры она единственная
 - ``documentVersion`` = ``utd820_05_01_02_hyphen`` — версия формата, в примере указана для приказа №820
 - ``titleIndex`` = ``0`` — номер титула, для счета-фактуры указан 0, потому что счет-фактура — однотитульный документ, и вторая сторона (получатель) свой титул не отправляет

2. Подготовим контент для титула.

 Титул — это XML-файл, соответствующий XSD-схеме.

 Некоторые данные в титуле может заполнить только пользователь — это информация о товарах, услугах и т.д. Остальные данные могут быть заполнены автоматически на основании формата документа и информации в Диадоке, например, реквизиты организации продавца и покупателя по идентификатору ящика, значения КНД, версии формата, версии программы и т.д.

 Чтобы упростить процесс генерации для пользователя, Диадок позволяет заполнить только «пользовательский» XML-файл, он же ``UserDataXml``. На его основе метод генерации сформирует основной титул, автоматически дополнив его всеми необходимыми данными согласно XSD-схеме.

 Схема работы:

	.. image:: ../_static/img/diadoc-api-generate-xml-schema1.png
		:align: center

 Как формировать ``UserDataXml`` — решает разработчик интеграционного решения. Один из вариантов — это кодогенерация из XSD-схемы упрощенного титула. Ссылка на схему находится в поле ``UserDataXsdUrl`` в теле ответа метода ``GetDocumentTypes``, приведенного выше.

 В C# SDK для всех версий формата приказа №820 есть `пример кодогенерации <https://github.com/diadoc/diadocsdk-csharp/tree/master/src/DataXml>`_. 
 Кодогенерация осуществлена `инструментом xsd.exe <https://docs.microsoft.com/ru-ru/dotnet/standard/serialization/xml-schema-definition-tool-xsd-exe>`_.
 Чтобы воспользоваться ей в C#-клиенте, нужно заполнить объект ``UniversalTransferDocument`` для титула отправителя или ``UniversalTransferDocumentBuyerTitle`` для титула получателя и `сериализовать его в XML <https://github.com/diadoc/diadocsdk-csharp/blob/master/src/XmlSerializerExtensions.cs>`_.

3. Получим титул счета-фактуры.

 Имея идентификаторы типа, функции, версии, порядкового номера титула и пользовательский контент, мы можем получить сам титул счета-фактуры.

*Пример HTTP-запроса*:

.. sourcecode:: http

    POST /GenerateTitleXml?boxId=a96be310-0982-461a-8b2a-91d198b7861c&documentTypeNamedId=Invoice&documentFunction=default&documentVersion=utd820_05_01_02_hyphen&titleIndex=0 HTTP/1.1
    Host: diadoc-api.kontur.ru
    Authorization: DiadocAuth ddauth_api_client_id={{ключ разработчика}}, ddauth_token={{авторизационный токен}}
    Content-Type: application/xml; charset=utf-8

*Пример тела запроса (UserDataXml)*:

.. sourcecode:: xml

	<?xml version="1.0" encoding="utf-8"?>
	<UniversalTransferDocumentWithHyphens Function="СЧФ"
			DocumentDate="01.08.2019"
			DocumentNumber="140"
			DocumentCreator="1"
			DocumentCreatorBase="1"
			CircumFormatInvoice="1"
			Currency="643" >
		<Sellers>
			<Seller>
				<OrganizationDetails OrgType="2"
						Inn="114500647890"
						FnsParticipantId="2BM-participantId1"
						OrgName="ИП Продавец Иван Иванович">
					<Address>
						<RussianAddress Region="02"/>
					</Address>
				</OrganizationDetails>
			</Seller>
		</Sellers>
		<Buyers>
			<Buyer>
				<OrganizationReference OrgType="1"
						BoxId="53d55d52-9317-4ad4-a7d9-5e9dd3cd6367"/>
			</Buyer>
		</Buyers>
		<Table TotalWithVatExcluded="0" Vat="0" Total="0">
			<Item Product="Товарная позиция"
					Unit="796"
					Quantity="0"
					Price="0"
					TaxRate="без НДС"
					SubtotalWithVatExcluded="0"
					Vat="0"
					Subtotal="0"
					Excise="10"/>
		</Table>
		<TransferInfo OperationInfo="Товары переданы"/>
		<Signers>
			<SignerDetails Inn="123456789047"
					LastName="Подписантов"
					FirstName="Иван"
					MiddleName="Иванович"
					RegistrationCertificate="1"
					SignerPowers="0"
					SignerType="3"
					SignerStatus="1"
					SignerPowersBase="Должностные обязанности"/>
		</Signers>
	</UniversalTransferDocumentWithHyphens>

*Пример тела ответа*:

::

    HTTP/1.1 200 OK

	<?xml version="1.0" encoding="windows-1251"?>
	<Файл ИдФайл="ON_NSCHFDOPPR_2BM-9670670494-967001000-202201240241297341956_2BM-participantId1_20220303_c1ffd60b-0925-4e08-a133-cc55e9fc5b3b" ВерсФорм="5.01" ВерсПрог="Diadoc 1.0">
	  <СвУчДокОбор ИдОтпр="2BM-participantId1" ИдПол="2BM-9670670494-967001000-202201240241297341956">
		<СвОЭДОтпр ИННЮЛ="6663003127" ИдЭДО="2BM" НаимОрг="АО &quot;ПФ &quot;СКБ Контур&quot;" />
	  </СвУчДокОбор>
	  <Документ КНД="1115131" ВремИнфПр="09.16.16" ДатаИнфПр="03.03.2022" НаимЭконСубСост="1" Функция="СЧФ" ОснДоверОргСост="1">
		<СвСчФакт НомерСчФ="140" ДатаСчФ="01.08.2019" КодОКВ="643">
		  <СвПрод>
			<ИдСв>
			  <СвИП ИННФЛ="114500647890">
				<ФИО Фамилия="Продавец" Имя="Иван" Отчество="Иванович" />
			  </СвИП>
			</ИдСв>
			<Адрес>
			  <АдрРФ КодРегион="02" />
			</Адрес>
		  </СвПрод>
		  <СвПокуп>
			<ИдСв>
			  <СвЮЛУч НаимОрг="Документация-получатель" ИННЮЛ="9670670494" КПП="967001000" />
			</ИдСв>
			<Адрес>
			  <АдрРФ Индекс="777777" КодРегион="50" Город="г. Москва" />
			</Адрес>
		  </СвПокуп>
		  <ДопСвФХЖ1 НаимОКВ="Российский рубль" ОбстФормСЧФ="1" />
		</СвСчФакт>
		<ТаблСчФакт>
		  <СведТов НомСтр="1" НаимТов="Товарная позиция" ОКЕИ_Тов="796" КолТов="0" ЦенаТов="0.00" СтТовБезНДС="0.00" НалСт="без НДС" СтТовУчНал="0.00">
			<Акциз>
			  <СумАкциз>10.00</СумАкциз>
			</Акциз>
			<СумНал>
			  <СумНал>0.00</СумНал>
			</СумНал>
			<ДопСведТов НаимЕдИзм="шт" />
		  </СведТов>
		  <ВсегоОпл СтТовБезНДСВсего="0.00" СтТовУчНалВсего="0.00">
			<СумНалВсего>
			  <СумНал>0.00</СумНал>
			</СумНалВсего>
		  </ВсегоОпл>
		</ТаблСчФакт>
		<СвПродПер>
		  <СвПер СодОпер="Товары переданы">
			<ОснПер НаимОсн="Без документа-основания" />
		  </СвПер>
		</СвПродПер>
		<Подписант ОснПолн="Должностные обязанности" ОблПолн="0" Статус="1">
		  <ФЛ ИННФЛ="123456789047">
			<ФИО Фамилия="Подписантов" Имя="Иван" Отчество="Иванович" />
		  </ФЛ>
		</Подписант>
	  </Документ>
	</Файл>
	
Полученное тело ответа содержит XML-файл первого титула документа.

Генерация последующих титулов
-----------------------------

Если тип документа содержит более одного титула и нужно сгенерировать титулы для последующих участников (т.е. когда ``titleIndex`` > 0), то сценарий аналогичен примеру выше, за исключением дополнительных параметров в запросе.

В большинстве случаев в контенте последующих титулов нужна информация из предыдущих, поэтому в запрос нужно передать идентификаторы уже существующего в Диадоке документа (``letterId`` + ``documentId``).

Генерация титула с настройкой редактирования
--------------------------------------------

Если при создании документа заданы :ref:`настройки редактирования <template_editing_settings>`, то валидация сгенерированного файла будет выполняться по XSD-схеме, соответствующей указанной настройке редактирования. То есть если настройка редактирования позволяет не указывать какой-либо атрибут, то с помощью метода ``GenerateTitleXml`` можно сгенерировать XML-файл, в котором этот атрибут будет отсутствовать. Валидация такого файла будет осуществлятся так, как будто неуказанный атрибут является опциональным по XSD-схеме.

.. _generate_title_xml_poa:

Генерация титула с машиночитаемой доверенностью
-----------------------------------------------

Чтобы сгенерировать титул с машиночитаемой доверенностью (МЧД), нужно указать информацию о МЧД для подписанта при формировании упрощенного титула ``UserDataXml``. Сделать это можно следующим образом:

- если детали подписанта генерируются по сертификату ``SignerReference``, то необходимо заполнить структуру ``PowerOfAttorney``: указать регистрационный номер МЧД и ИНН доверителя или использовать МЧД по умолчанию;

- если при генерации детали подписанта задаются в явном виде с помощью структуры ``SignerDetails``, то в случае формирования подписанта по МЧД интегратор сам определяет необходимость использования ИНН подписанта и название организации для ЮЛ из МЧД.

*Структура PowerOfAttorney в XSD-схеме*

.. sourcecode:: xml

	<xs:complexType name="PowerOfAttorney">
	<xs:sequence>
	  <xs:element name="FullId" minOccurs="0">
		<xs:complexType>
		  <xs:attribute name="RegistrationNumber" use="required" type="guid"/>
		  <xs:attribute name="IssuerInn" use="required" type="inn"/>
		</xs:complexType>
	  </xs:element>
	</xs:sequence>
	<xs:attribute name="UseDefault" use="required">
	  <xs:simpleType>
		<xs:restriction base="xs:string">
		  <xs:enumeration value="true" />
		  <xs:enumeration value="false" />
		</xs:restriction>
	  </xs:simpleType>
	</xs:attribute>
	</xs:complexType>

*Пример тела запроса для документа с МЧД*

.. sourcecode:: xml

	<?xml version="1.0" encoding="utf-8"?>
	<UniversalTransferDocumentWithHyphens Function="СЧФ"
			DocumentDate="01.08.2019"
			DocumentNumber="140"
			DocumentCreator="1"
			DocumentCreatorBase="1"
			CircumFormatInvoice="1"
			Currency="643" >
		<Sellers>
			<Seller>
				<OrganizationDetails OrgType="2"
						Inn="114500647890"
						FnsParticipantId="2BM-participantId1"
						OrgName="ИП Продавец Иван Иванович">
					<Address>
						<RussianAddress Region="02"/>
					</Address>
				</OrganizationDetails>
			</Seller>
		</Sellers>
		<Buyers>
			<Buyer>
				<OrganizationReference OrgType="1"
						BoxId="53d55d52-9317-4ad4-a7d9-5e9dd3cd6367"/>
			</Buyer>
		</Buyers>
		<Table TotalWithVatExcluded="0" Vat="0" Total="0">
			<Item Product="Товарная позиция"
					Unit="796"
					Quantity="0"
					Price="0"
					TaxRate="без НДС"
					SubtotalWithVatExcluded="0"
					Vat="0"
					Subtotal="0"
					Excise="10"/>
		</Table>
		<TransferInfo OperationInfo="Товары переданы"/>
		<Signers>
			<SignerReference BoxId="74ef3a00-c625-3ef0-9b50-65bf7f96b9ae" CertificateThumbprint="8A80C2723DBC4F0A94F8CEE21C0A15A68A80C272">
				<PowerOfAttorney UseDefault="false">
					<FullId RegistrationNumber="4F73C574-CF7C-4664-91B9-48185BC66A27" IssuerInn="114500647890" />
				</PowerOfAttorney> 
			</SignerReference>
		</Signers>
	</UniversalTransferDocumentWithHyphens>

*Пример тела ответа*

::

    HTTP/1.1 200 OK

	<?xml version="1.0" encoding="windows-1251"?>
    <Файл ИдФайл="ON_NSCHFDOPPR_2BM-9670670494-967001000-202201240241297341956_2BM-participantId1_20220303_c1ffd60b-0925-4e08-a133-cc55e9fc5b3b" ВерсФорм="5.01" ВерсПрог="Diadoc 1.0">
      <СвУчДокОбор ИдОтпр="2BM-participantId1" ИдПол="2BM-9670670494-967001000-202201240241297341956">
            <СвОЭДОтпр ИННЮЛ="6663003127" ИдЭДО="2BM" НаимОрг="АО &quot;ПФ &quot;СКБ Контур&quot;" />
      </СвУчДокОбор>
      <Документ КНД="1115131" ВремИнфПр="09.16.16" ДатаИнфПр="03.03.2022" НаимЭконСубСост="1" Функция="СЧФ" ОснДоверОргСост="1">
            <СвСчФакт НомерСчФ="140" ДатаСчФ="01.08.2019" КодОКВ="643">
              <СвПрод>
                    <ИдСв>
                      <СвИП ИННФЛ="114500647890">
                            <ФИО Фамилия="Продавец" Имя="Иван" Отчество="Иванович" />
                      </СвИП>
                    </ИдСв>
                    <Адрес>
                      <АдрРФ КодРегион="02" />
                    </Адрес>
              </СвПрод>
              <СвПокуп>
                    <ИдСв>
                      <СвЮЛУч НаимОрг="Документация-получатель" ИННЮЛ="9670670494" КПП="967001000" />
                    </ИдСв>
                    <Адрес>
                      <АдрРФ Индекс="777777" КодРегион="50" Город="г. Москва" />
                    </Адрес>
              </СвПокуп>
              <ДопСвФХЖ1 НаимОКВ="Российский рубль" ОбстФормСЧФ="1" />
            </СвСчФакт>
            <ТаблСчФакт>
              <СведТов НомСтр="1" НаимТов="Товарная позиция" ОКЕИ_Тов="796" КолТов="0" ЦенаТов="0.00" СтТовБезНДС="0.00" НалСт="без НДС" СтТовУчНал="0.00">
                    <Акциз>
                      <СумАкциз>10.00</СумАкциз>
                    </Акциз>
                    <СумНал>
                      <СумНал>0.00</СумНал>
                    </СумНал>
                    <ДопСведТов НаимЕдИзм="шт" />
              </СведТов>
              <ВсегоОпл СтТовБезНДСВсего="0.00" СтТовУчНалВсего="0.00">
                    <СумНалВсего>
                      <СумНал>0.00</СумНал>
                    </СумНалВсего>
              </ВсегоОпл>
            </ТаблСчФакт>
            <СвПродПер>
              <СвПер СодОпер="Товары переданы">
                    <ОснПер НаимОсн="Без документа-основания" />
              </СвПер>
            </СвПродПер>
            <Подписант ОснПолн="Должностные обязанности" ОблПолн="0" Статус="1">
              <ЮЛ ИННЮЛ="114500647890" Должн="Сотрудник" НаимОрг="Тестовая организация">
					<ФИО Фамилия="Тестовый" Имя="Сертификат" Отчество="Сертификатович" />
			</ЮЛ>
            </Подписант>
      </Документ>
    </Файл>