Генерация формализованного документа
====================================

.. contents:: :local:
	:depth: 3

Через Диадок можно отправить как формализованные, так и неформализованные документы. Неформализованные документы могут быть представлены в любом формате. Формализованные документы должны представлять собой XML-файлы в формате, рекомендованном ФНС.

Вы можете сформировать формализованный документ самостоятельно или воспользоваться методом API :doc:`../http/GenerateTitleXml` для генерации документа с заданными параметрами.

Чтобы сгенерировать документ методом ``GenerateTitleXml``, нужно передать в метод следующие параметры:

	- ``documentTypeNamedId`` — тип документа;
	- ``documentFunction`` — функция документа;
	- ``documentVersion`` — версия документа;
	- ``titleIndex`` — идентификатор титула документа, т.е. порядковый номер титула, пронумерованный с ``0``;

А в теле запроса метода нужно передать XML-файл ``UserDataXml``, соответствующий XSD-схеме ``UsedDataXsd``.

Получить все эти значения можно с помощью метода :doc:`../http/GetDocumentTypes`. Инструкция о получении данных для титула из метода ``GetDocumentTypes`` приведена в разделе :ref:`doctype_title`.

Метод ``GenerateTitleXml`` вернет в ответе XML-файл титула, сгенерированный в соответствии с указанной XSD-схемой. Дальше полученный файл можно:

	- :ref:`подготовить к подписанию <doc_prepare_to_sign>`, подписать и :ref:`отправить <doc_send>`,
	- :ref:`сохранить и отправить позже <doc_delaysend>`,
	- :ref:`сохранить как черновик <doc_draft>`.


Генерация титула отправителя
----------------------------

Ниже описан алгоритм для генерации титула отправителя.

В качестве примера используется УПД формата приказа ФНС № 970, но описанный алгоритм применим и к другим форматам документов.

#. Получение типа и версии документа.

   Найти тип и версию документа можно с помощью метода :doc:`../http/GetDocumentTypes`. Инструкция о получении данных для титула из метода ``GetDocumentTypes`` приведена в разделе :ref:`doctype_title`.

   Из ответа метода ``GetDocumentTypes`` получаем следующие значения для параметров метода ``GenerateTitleXml``:

    - ``documentTypeNamedId`` = ``UniversalTransferDocument`` — имя типа документа,
    - ``documentFunction`` = ``СЧФ`` — функция документа,
    - ``documentVersion`` = ``utd970_05_02_01`` — версия формата,
    - ``titleIndex`` = ``0`` — номер титула.

#. Подготовка содержимого титула.

   XML-файл титула должен быть заполнен в соответствии с XSD-схемой, установленной ФНС.

   Некоторые данные в титуле может заполнить только пользователь — это информация о товарах, услугах и т.д. Остальные данные могуть быть заполнены автоматически на основании формата документа и информации в Диадоке, — например, реквизиты организации продавца и покупателя по идентификатору ящика, значения КНД, версии формата, версии программы и т.д.

   Чтобы упростить процесс заполнения данных для пользователя, Диадок позволяет заполнить только «пользовательскую часть» XML-файла титула — упрощенный XML-файл ``UserDataXml``. На его основе метод генерации сформирует основной титул, автоматически дополнив его всеми необходимыми данными согласно XSD-схеме.

   Чтобы сформировать упрощенный XML-файл ``UserDataXml`` нужно использовать XSD-схему ``UsedDataXsd``, — она содержит информацию для генерации пользовательской части титула. Получить ``UsedDataXsd`` можно с помощью метода ``GetDocumentTypes``. Инструкция о получении данных для титула из метода ``GetDocumentTypes`` приведена в разделе :ref:`doctype_title`.

   Схема работы:

	.. image:: ../_static/img/diadoc-api-generate-xml-schema1.png
		:align: center

   Как сформировать ``UserDataXml`` — решает разработчик интеграционного решения. Один из вариантов — это кодогенерация XML на основе XSD-схемы упрощенного титула. 

   В C# SDK для всех версий форматов приказов №820 и №970 есть `пример кодогенерации <https://github.com/diadoc/diadocsdk-csharp/tree/master/src/DataXml>`_ титулов.
   Кодогенерация осуществляется `инструментом xsd.exe <https://docs.microsoft.com/ru-ru/dotnet/standard/serialization/xml-schema-definition-tool-xsd-exe>`_.
   Чтобы воспользоваться ей в C#-клиенте, нужно заполнить объект ``UniversalTransferDocument`` для титула отправителя или ``UniversalTransferDocumentBuyerTitle`` для титула получателя и `сериализовать его в XML <https://github.com/diadoc/diadocsdk-csharp/blob/master/src/XmlSerializerExtensions.cs>`_.

#. Генерация титула.

   Титул генерируется с помощью метода :doc:`../http/GenerateTitleXml`. В него нужно передать полученные на предыдущих этапах параметры: тип, функцию, версию, порядковый номер титула и содержимое ``UserDataXml``.

   Тело ответа, полученное в результате выполнения метода, содержит XML-файл первого титула документа.

   **Пример HTTP-запроса метода GenerateTitleXml:**

   .. code-block:: http

		 POST /GenerateTitleXml?boxId=74ef3a00-c625-4ef0-9b50-65bf7f96b9ae&documentTypeNamedId=UniversalTransferDocument&documentFunction=СЧФ&documentVersion=utd970_05_02_01&titleIndex=0 HTTP/1.1
		 Host: diadoc-api.kontur.ru
		 Authorization: DiadocAuth ddauth_api_client_id={{ключ разработчика}}, ddauth_token={{авторизационный токен}}
		 Content-Type: application/xml; charset=utf-8

   **Пример тела запроса метода GenerateTitleXml (UserDataXml) для формата 970:**

   .. container:: toggle

	.. code-block:: xml

		<?xml version="1.0" encoding="utf-8"?>
		<UniversalTransferDocument DocumentDate="01.02.2003" DocumentNumber="444" Currency="643" Function="СЧФ" Uid="Уид" ApprovedStructureAdditionalInfoFields="1111.2222.0000" SenderFnsParticipantId="2BM-9616675014-961601000-202310240839360601227" RecipientFnsParticipantId="2BM-966259685098-20231024083946535138700000000" FileIdSeller="СвСчФакт-ИмяФайлИспрПрод" FileIdBuyer="СвСчФакт-ИмяФайлИспрПок" CurrencyRate="12" GovernmentContractInfo="1234567890123456789012345" DocumentCreator="Документ-НаимЭконСубСост" CircumFormat="1" xmlns:xs="http://www.w3.org/2001/XMLSchema">
			<Sellers>
				<Seller>
					<OrganizationDetails Okpo="0166273597" Okopf="12200" FullNameOkopf="СвПрод-ПолнНаимОПФ" Department="СвПрод-СтруктПодр" OrganizationAdditionalInfo="СвПрод-ИнфДляУчаст" ShortOrgName="СвПрод-СокрНаим" OtherContactInfo="Контакт-ИнКонт" CorrespondentAccount="30101810500000000641" BankAccountNumber="49634485849155" BankName="СИБИРСКИЙ БАНК ПАО СБЕРБАНК" BankId="045004641" OrgType="2" OrgName="СвЮЛУч-НаимОрг" Inn="9103624367" Kpp="187245452">
						<Phones>
							<Phone>8-343-123-4567</Phone>
						</Phones>
						<Emails>
							<Email>pochta@google.com</Email>
						</Emails>
						<Address>
							<RussianAddress Region="66" ZipCode="344249" Territory="Тюмень" City="Тюмень" Locality="АдрРФ-НаселПункт" Street="АдрРФ-Улица" Building="АдрРФ-Дом" Block="АдрРФ-Корпус" Apartment="АдрРФ-Кварт" OtherInfo="АдрРФ-ИныеСвед" />
						</Address>
					</OrganizationDetails>
				</Seller>
			</Sellers>
			<Shippers>
				<Shipper>
					<OrganizationDetails Okpo="76098674" Okopf="12000" FullNameOkopf="ГрузОтпр-ПолнНаимОПФ" Department="ГрузОтпр-СтруктПодр" OrganizationAdditionalInfo="ГрузОтпр-ИнфДляУчаст" ShortOrgName="ГрузОтпр-СокрНаим" OrgType="1" OrgName="Иванов Иван Иванович" Inn="753381367749" Ogrn="421319982803452" OgrnDate="12.12.2012" IndividualEntityRegistrationCertificate="СвИП-СвГосРегИП" OrganizationOrPersonInfo="СвИП-ИныеСвед">
						<Address>
							<GarAddress AddressCode="03510210-e5f3-4bc6-bbd2-24d7fe25b3ed" Region="66" ZipCode="450133" LandPlot="ЗемелУчасток">
								<MunicipalTerritory Type="1" NameOrNumber="МуниципРайон-Наим" />
								<UrbanSettlement Type="1" NameOrNumber="ГородСелПоселен-Наим" />
								<Locality Type="НаселенПункт" NameOrNumber="НаселенПункт-Наим" />
								<ElementPlanningStructure Type="ЭлПланСтруктур" NameOrNumber="ЭлПланСтруктур-Наим" />
								<ElementRoadNetwork Type="ЭлУлДорСети" NameOrNumber="ЭлУлДорСети-Наим" />
								<Buildings>
									<Building Type="Здание" NameOrNumber="Здание-Номер" />
								</Buildings>
								<RoomBuilding Type="ПомещЗдания" NameOrNumber="ПомещЗдания-Номер" />
								<RoomApartment Type="ПомещКвартиры" NameOrNumber="ПомещКвартиры-Номер" />
							</GarAddress>
						</Address>
					</OrganizationDetails>
				</Shipper>
			</Shippers>
			<Consignees>
				<Consignee>
					<OrganizationDetails Okopf="12000" FullNameOkopf="ГрузПолуч-ПолнНаимОПФ" Department="ГрузПолуч-СтруктПодр" OrganizationAdditionalInfo="ГрузПолуч-ИнфДляУчаст" ShortOrgName="ГрузПолуч-СокрНаим" BankAccountNumber="569712456874" BankName="ЗАО Сбербанк России, отделение на Московской 11" BankId="012345671" OrgType="3" OrgName="Петров Петр Петрович" Inn="518191632595" PersonStatusId="1" OrganizationOrPersonInfo="СвФЛУч-ИныеСвед">
						<Address>
							<ForeignAddress Country="112" Address="АдрИнф-АдрТекст" />
						</Address>
					</OrganizationDetails>
				</Consignee>
			</Consignees>
			<PaymentDocuments>
				<Document Number="СЧФ/123/456" Date="01.02.2003" Total="1000" />
			</PaymentDocuments>
			<DocumentShipments>
				<DocumentShipment DocumentName="Документ о передаче товаров (работ, услуг, имущественных прав)" DocumentNumber="444" DocumentDate="01.02.2003">
					<IdentificationDetails Inn="1978337389" />
				</DocumentShipment>
			</DocumentShipments>
			<Buyers>
				<Buyer>
					<OrganizationDetails Okpo="74047744" Okopf="12200" FullNameOkopf="СвПокуп-ПолнНаимОПФ" Department="СвПокуп-СтруктПодр" OrganizationAdditionalInfo="СвПокуп-ИнфДляУчаст" ShortOrgName="СвПокуп-СокрНаим" OrgType="2" OrgName="СвЮЛУч-НаимОрг" Inn="1234567894" Kpp="667301001">
						<Address>
							<ForeignAddress Country="112" Address="АдрИнф-АдрТекст" />
						</Address>
					</OrganizationDetails>
				</Buyer>
			</Buyers>
			<CommitmentTypes>
				<CommitmentType CommitmentTypeCode="1" CommitmentTypeName="ВидОбяз-НаимВидОбяз" />
			</CommitmentTypes>
			<SellerInfoCircumPublicProc DateStateContract="02.02.2002" NumberStateContract="5" SellerTreasuryCode="0160" />
			<FactorInfo>
				<OrganizationDetails Okpo="74047744" Okopf="12000" FullNameOkopf="СвФактор-ПолнНаимОПФ" Department="СвФактор-СтруктПодр" OrganizationAdditionalInfo="СвФактор-ИнфДляУчаст" ShortOrgName="СвФактор-СокрНаим" OrgType="1" OrgName="ФИО-Фамилия ФИО-Имя ФИО-Отчество" Inn="916363626153" Ogrn="421032906553286" OgrnDate="21.08.2019" OrganizationOrPersonInfo="СвИП-ИныеСвед">
					<Address>
						<RussianAddress Region="66" ZipCode="344249" Territory="Тюмень" City="Тюмень" Locality="АдрРФ-НаселПункт" Street="АдрРФ-Улица" Building="АдрРФ-Дом" Block="АдрРФ-Корпус" Apartment="АдрРФ-Кварт" OtherInfo="АдрРФ-ИныеСвед" />
					</Address>
				</OrganizationDetails>
			</FactorInfo>
			<MainAssignMonetaryClaim DocumentName="ОснУстДенТреб-РеквНаимДок" DocumentNumber="144" DocumentDate="04.04.2004">
				<IdentificationDetails Inn="342265432525" />
			</MainAssignMonetaryClaim>
			<AccompanyingDocuments>
				<AccompanyingDocument DocumentName="СопрДокФХЖ-РеквНаимДок" DocumentNumber="876" DocumentDate="05.05.2005">
					<IdentificationDetails StatusId="PhysicalPerson" Country="112" OrgName="ДаннИно-Наим" LegalEntityId="ДаннИно-Идентиф" OrganizationOrPersonInfo="ДаннИно-ИныеСвед" />
				</AccompanyingDocument>
			</AccompanyingDocuments>
			<AdditionalInfoId InfoFileId="5b0a8e80-1a7b-4194-a64d-60ca9f10dd82">
				<AdditionalInfo Id="ТекстИнф-Идентиф" Value="ТекстИнф-Идентиф" />
			</AdditionalInfoId>
			<Table TotalWithVatExcluded="8965" Vat="456.00" Total="10000">
				<Item TaxRate="TwentyPercent" Product="СведТов-НаимТов" Unit="113" UnitName="м" Quantity="16" Price="200" SubtotalWithVatExcluded="654" Vat="1000.000000000000000" RestoredVat="550" Subtotal="784.8" ItemMark="5" AdditionalProperty="Приз" ItemToRelease="102" ItemKind="СортТов" ItemSeries="ДопСведТов-СерияТов" Gtin="10000057074365" ItemTypeCode="1111111111" ProductTypeCode="676">
					<CustomsDeclarations>
						<CustomsDeclaration Country="980" DeclarationNumber="123456" />
					</CustomsDeclarations>
					<AccompanyingDocuments>
						<AccompanyingDocument DocumentName="СопрДокТов-РеквНаимДок" DocumentNumber="144" DocumentDate="04.04.2004">
							<IdentificationDetails Inn="342265432525" />
						</AccompanyingDocument>
					</AccompanyingDocuments>
					<DepreciationInfo DepreciationGroup="13" Okof="165" UsefulPeriod="23" ActualPeriod="100" />
					<ItemTracingInfos>
						<ItemTracingInfo RegNumberUnit="10001000/010123/1234567/001" Unit="778" Quantity="30" PriceWithVatExcluded="100" />
					</ItemTracingInfos>
					<ItemIdentificationNumbers>
						<ItemIdentificationNumber TransPackageId="НомСредИдентТов-ИдентТрансУпак" QuantityMark="100" BatchMarkCode="111">
							<Unit>НомСредИдентТов-КИЗ</Unit>
						</ItemIdentificationNumber>
					</ItemIdentificationNumbers>
				</Item>
				<Item TaxRate="TwentyPercent" Product="Product2 &gt; 2.0 мм" Unit="778" UnitName="уп" Quantity="114.100" Price="516.67" SubtotalWithVatExcluded="58951.67" Vat="1000" RestoredVat="1345" Subtotal="70742.00" ItemMark="5" AdditionalProperty="ДопП" ItemVendorCode="ДопСведТов-КодТов" ItemToRelease="505" ItemCharact="ДопСведТов-ХарактерТов" ItemArticle="ДопСведТов-АртикулТов" ItemKind="СортТов" ItemSeries="ДопСведТов-СерияТов" Gtin="10000057074365" ItemTypeCode="1111111111">
					<CustomsDeclarations>
						<CustomsDeclaration Country="178" DeclarationNumber="555555" />
					</CustomsDeclarations>
					<DepreciationInfo DepreciationGroup="12" Okof="165" UsefulPeriod="234" ActualPeriod="100" />
				</Item>
			</Table>
			<TransferInfo OperationInfo="СвПер-СодОпер" OperationType="СвПер-ВидОпер" TransferDate="15.02.2020" TransferStartDate="16.02.2020" TransferEndDate="16.02.2021">
				<CreatedThingTransferDocument DocumentName="ДокПерВещ-РеквНаимДок" DocumentNumber="098" DocumentDate="03.02.2020">
					<IdentificationDetails Inn="4620212891" />
				</CreatedThingTransferDocument>
				<TransferBases>
					<TransferBase DocumentName="ОснПер-РеквНаимДок" DocumentNumber="567" DocumentDate="14.02.2020">
						<IdentificationDetails Inn="144647873819" />
					</TransferBase>
				</TransferBases>
				<OtherIssuer LastName="Иванов" FirstName="Иван" MiddleName="Иванович" Position="ПредОргПер-Должность" EmployeeInfo="ПредОргПер-ИныеСвед" OrganizationName="ПредОргПер-НаимОргПер">
					<EmployeeBase DocumentName="ОснПолнПредПер-РеквНаимДок" DocumentNumber="098" DocumentDate="03.02.2020">
						<IdentificationDetails Inn="4620212891" />
					</EmployeeBase>
					<OrganizationBase DocumentName="ОснДоверОргПер-РеквНаимДок" DocumentNumber="098" DocumentDate="03.02.2020">
						<IdentificationDetails Inn="4620212891" />
					</OrganizationBase>
				</OtherIssuer>
				<AdditionalInfoId InfoFileId="9c3adc2b-a085-4acd-af8c-3494290d782c">
					<AdditionalInfo Id="Идентиф1в" Value="Значен1в" />
					<AdditionalInfo Id="Идентиф2в" Value="Значен2в" />
				</AdditionalInfoId>
			</TransferInfo>
			<Signers>
				<Signer SignatureType="1" SignerPowersConfirmationMethod="3" SigningDate="21.01.2024">
					<Fio FirstName="Петр" LastName="Петров" MiddleName="Петрович" />
					<Position PositionSource="Manual">Подписант-Должн</Position>
					<SignerAdditionalInfo SignerAdditionalInfoSource="Manual">Подписант-ДопСведПодп</SignerAdditionalInfo>
					<PowerOfAttorney>
						<Electronic>
						<Manual RegistrationNumber="4a743152-e772-4249-9a47-e2e290258e79" RegistrationDate="17.09.2018" InternalNumber="123" InternalDate="18.09.2018" SystemId="СвДоверЭл-ИдСистХран" SystemUrl="СвДоверЭл-УРЛСист" />
						</Electronic>
					</PowerOfAttorney>
				</Signer>
			</Signers>
			<DocumentCreatorBase DocumentName="ОснДоверОргСост-РеквНаимДок" DocumentNumber="123" DocumentDate="01.02.2003">
				<IdentificationDetails StatusId="PhysicalPerson" Country="112" OrgName="ДаннИно-Наим" LegalEntityId="ДаннИно-Идентиф" OrganizationOrPersonInfo="ДаннИно-ИныеСвед" />
			</DocumentCreatorBase>
		</UniversalTransferDocument>

   **Пример тела ответа метода GenerateTitleXml:**

   .. container:: toggle

	.. code-block:: xml

		HTTP/1.1 200 OK

		<?xml version="1.0" encoding="windows-1251"?>
		<Файл ИдФайл="ON_NSCHFDOPPR_2BM-966259685098-20231024083946535138700000000_2BM-9616675014-961601000-202310240839360601227_20240422_228cc7ce-ddd1-47b6-bcba-ca087007d5bc_1_1_0_0_1_00" ВерсФорм="5.02" ВерсПрог="Diadoc 1.0">
			<Документ КНД="1115131" ВремИнфПр="18.47.57" ДатаИнфПр="22.04.2024" Функция="СЧФ" УИД="Уид" НаимЭконСубСост="Документ-НаимЭконСубСост" СоглСтрДопИнф="1111.2222.0000">
				<СвСчФакт НомерДок="444" ДатаДок="01.02.2003" ИмяФайлИспрПрод="СвСчФакт-ИмяФайлИспрПрод" ИмяФайлИспрПок="СвСчФакт-ИмяФайлИспрПок">
					<СвПрод ОКПО="0166273597" КодОПФ="12200" ПолнНаимОПФ="СвПрод-ПолнНаимОПФ" СтруктПодр="СвПрод-СтруктПодр" ИнфДляУчаст="СвПрод-ИнфДляУчаст" СокрНаим="СвПрод-СокрНаим">
						<ИдСв>
							<СвЮЛУч НаимОрг="СвЮЛУч-НаимОрг" ИННЮЛ="9103624367" КПП="187245452" />
						</ИдСв>
						<Адрес>
							<АдрРФ КодРегион="66" НаимРегион="Свердловская область" Индекс="344249" Район="Тюмень" Город="Тюмень" НаселПункт="АдрРФ-НаселПункт" Улица="АдрРФ-Улица" Дом="АдрРФ-Дом" Корпус="АдрРФ-Корпус" Кварт="АдрРФ-Кварт" ИныеСвед="АдрРФ-ИныеСвед" />
						</Адрес>
						<БанкРекв НомерСчета="49634485849155">
							<СвБанк НаимБанк="СИБИРСКИЙ БАНК ПАО СБЕРБАНК" БИК="045004641" КорСчет="30101810500000000641" />
						</БанкРекв>
						<Контакт ИнКонт="Контакт-ИнКонт">
							<Тлф>8-343-123-4567</Тлф>
							<ЭлПочта>pochta@google.com</ЭлПочта>
						</Контакт>
					</СвПрод>
					<ГрузОт>
						<ГрузОтпр ОКПО="76098674" КодОПФ="12000" ПолнНаимОПФ="ГрузОтпр-ПолнНаимОПФ" СтруктПодр="ГрузОтпр-СтруктПодр" ИнфДляУчаст="ГрузОтпр-ИнфДляУчаст" СокрНаим="ГрузОтпр-СокрНаим">
							<ИдСв>
								<СвИП ИННФЛ="753381367749" СвГосРегИП="СвИП-СвГосРегИП" ОГРНИП="421319982803452" ДатаОГРНИП="12.12.2012" ИныеСвед="СвИП-ИныеСвед">
									<ФИО Фамилия="Иванов" Имя="Иван" Отчество="Иванович" />
								</СвИП>
							</ИдСв>
							<Адрес>
								<АдрГАР ИдНом="03510210-e5f3-4bc6-bbd2-24d7fe25b3ed" Индекс="450133">
									<Регион>66</Регион>
									<НаимРегион>Свердловская область</НаимРегион>
									<МуниципРайон ВидКод="1" Наим="МуниципРайон-Наим" />
									<ГородСелПоселен ВидКод="1" Наим="ГородСелПоселен-Наим" />
									<НаселенПункт Вид="НаселенПункт" Наим="НаселенПункт-Наим" />
									<ЭлПланСтруктур Тип="ЭлПланСтруктур" Наим="ЭлПланСтруктур-Наим" />
									<ЭлУлДорСети Тип="ЭлУлДорСети" Наим="ЭлУлДорСети-Наим" />
									<ЗемелУчасток>ЗемелУчасток</ЗемелУчасток>
									<Здание Тип="Здание" Номер="Здание-Номер" />
									<ПомещЗдания Тип="ПомещЗдания" Номер="ПомещЗдания-Номер" />
									<ПомещКвартиры Тип="ПомещКвартиры" Номер="ПомещКвартиры-Номер" />
								</АдрГАР>
							</Адрес>
						</ГрузОтпр>
					</ГрузОт>
					<ГрузПолуч КодОПФ="12000" ПолнНаимОПФ="ГрузПолуч-ПолнНаимОПФ" СтруктПодр="ГрузПолуч-СтруктПодр" ИнфДляУчаст="ГрузПолуч-ИнфДляУчаст" СокрНаим="ГрузПолуч-СокрНаим">
						<ИдСв>
							<СвФЛУч ИННФЛ="518191632595" ИдСтатЛ="1" ИныеСвед="СвФЛУч-ИныеСвед">
								<ФИО Фамилия="Петров" Имя="Петр" Отчество="Петрович" />
							</СвФЛУч>
						</ИдСв>
						<Адрес>
							<АдрИнф КодСтр="112" НаимСтран="Беларусь" АдрТекст="АдрИнф-АдрТекст" />
						</Адрес>
						<БанкРекв НомерСчета="569712456874">
							<СвБанк НаимБанк="ЗАО Сбербанк России, отделение на Московской 11" БИК="012345671" />
						</БанкРекв>
					</ГрузПолуч>
					<СвПРД НомерПРД="СЧФ/123/456" ДатаПРД="01.02.2003" СуммаПРД="1000.00" />
					<ДокПодтвОтгрНом РеквНаимДок="Документ о передаче товаров (работ, услуг, имущественных прав)" РеквНомерДок="444" РеквДатаДок="01.02.2003">
						<РеквИдРекСост>
							<ИННЮЛ>1978337389</ИННЮЛ>
						</РеквИдРекСост>
					</ДокПодтвОтгрНом>
					<СвПокуп ОКПО="74047744" КодОПФ="12200" ПолнНаимОПФ="СвПокуп-ПолнНаимОПФ" СтруктПодр="СвПокуп-СтруктПодр" ИнфДляУчаст="СвПокуп-ИнфДляУчаст" СокрНаим="СвПокуп-СокрНаим">
						<ИдСв>
							<СвЮЛУч НаимОрг="СвЮЛУч-НаимОрг" ИННЮЛ="1234567894" КПП="667301001" />
						</ИдСв>
						<Адрес>
							<АдрИнф КодСтр="112" НаимСтран="Беларусь" АдрТекст="АдрИнф-АдрТекст" />
						</Адрес>
					</СвПокуп>
					<ДенИзм КодОКВ="643" НаимОКВ="Российский рубль" КурсВал="12" />
					<ДопСвФХЖ1 ИдГосКон="1234567890123456789012345" СпОбстФСЧФ="1">
						<ВидОбяз КодВидОбяз="1" НаимВидОбяз="ВидОбяз-НаимВидОбяз" />
						<ИнфПродЗаГосКазн ДатаГосКонт="02.02.2002" НомерГосКонт="5" КодКазначПрод="0160" />
						<СвФактор ОКПО="74047744" КодОПФ="12000" ПолнНаимОПФ="СвФактор-ПолнНаимОПФ" СтруктПодр="СвФактор-СтруктПодр" ИнфДляУчаст="СвФактор-ИнфДляУчаст" СокрНаим="СвФактор-СокрНаим">
							<ИдСв>
								<СвИП ИННФЛ="916363626153" ОГРНИП="421032906553286" ДатаОГРНИП="21.08.2019" ИныеСвед="СвИП-ИныеСвед">
									<ФИО Фамилия="ФИО-Фамилия" Имя="ФИО-Имя" Отчество="ФИО-Отчество" />
								</СвИП>
							</ИдСв>
							<Адрес>
								<АдрРФ КодРегион="66" НаимРегион="Свердловская область" Индекс="344249" Район="Тюмень" Город="Тюмень" НаселПункт="АдрРФ-НаселПункт" Улица="АдрРФ-Улица" Дом="АдрРФ-Дом" Корпус="АдрРФ-Корпус" Кварт="АдрРФ-Кварт" ИныеСвед="АдрРФ-ИныеСвед" />
							</Адрес>
						</СвФактор>
						<ОснУстДенТреб РеквНаимДок="ОснУстДенТреб-РеквНаимДок" РеквНомерДок="144" РеквДатаДок="04.04.2004">
							<РеквИдРекСост>
								<ИННФЛ>342265432525</ИННФЛ>
							</РеквИдРекСост>
						</ОснУстДенТреб>
						<СопрДокФХЖ РеквНаимДок="СопрДокФХЖ-РеквНаимДок" РеквНомерДок="876" РеквДатаДок="05.05.2005">
							<РеквИдРекСост>
								<ДаннИно КодСтр="112" НаимСтран="Беларусь" Наим="ДаннИно-Наим" ИдСтат="ИГ" ИныеСвед="ДаннИно-ИныеСвед" Идентиф="ДаннИно-Идентиф" />
							</РеквИдРекСост>
						</СопрДокФХЖ>
					</ДопСвФХЖ1>
					<ИнфПолФХЖ1 ИдФайлИнфПол="5b0a8e80-1a7b-4194-a64d-60ca9f10dd82">
						<ТекстИнф Идентиф="ТекстИнф-Идентиф" Значен="ТекстИнф-Идентиф" />
					</ИнфПолФХЖ1>
				</СвСчФакт>
				<ТаблСчФакт>
					<СведТов НомСтр="1" НалСт="20%" НаимТов="СведТов-НаимТов" ОКЕИ_Тов="113" НаимЕдИзм="м3" КолТов="16" ЦенаТов="200.00" СтТовБезНДС="654.00" СтТовУчНал="784.80">
						<СвДТ КодПроисх="980" НомерДТ="123456" />
						<ДопСведТов ПрТовРаб="5" ДопПризн="Приз" КрНаимСтрПр="Евросоюз" НадлОтп="102" СортТов="СортТов" СерияТов="ДопСведТов-СерияТов" ГТИН="10000057074365" КодВидТов="1111111111" КодВидПр="676">
							<СопрДокТов РеквНаимДок="СопрДокТов-РеквНаимДок" РеквНомерДок="144" РеквДатаДок="04.04.2004">
								<РеквИдРекСост>
									<ИННФЛ>342265432525</ИННФЛ>
								</РеквИдРекСост>
							</СопрДокТов>
							<НалУчАморт АмГруппа="13" КодОКОФ="165" СрПолИспОС="23" ФактСрокИсп="100" />
							<СумНалВосст>
								<СумНал>550.00</СумНал>
							</СумНалВосст>
							<СведПрослеж НомТовПрослеж="10001000/010123/1234567/001" ЕдИзмПрослеж="778" КолВЕдПрослеж="30" СтТовБезНДСПрослеж="100" НаимЕдИзмПрослеж="упак" />
							<НомСредИдентТов ИдентТрансУпак="НомСредИдентТов-ИдентТрансУпак" КолВедМарк="100" ПрПартМарк="111">
								<КИЗ>НомСредИдентТов-КИЗ</КИЗ>
							</НомСредИдентТов>
						</ДопСведТов>
						<Акциз>
							<БезАкциз>без акциза</БезАкциз>
						</Акциз>
						<СумНал>
							<СумНал>1000.00</СумНал>
						</СумНал>
					</СведТов>
					<СведТов НомСтр="2" НалСт="20%" НаимТов="Product2 &gt; 2.0 мм" ОКЕИ_Тов="778" НаимЕдИзм="упак" КолТов="114.100" ЦенаТов="516.67" СтТовБезНДС="58951.67" СтТовУчНал="70742.00">
						<СвДТ КодПроисх="178" НомерДТ="555555" />
						<ДопСведТов ПрТовРаб="5" ДопПризн="ДопП" КрНаимСтрПр="Конго" НадлОтп="505" ХарактерТов="ДопСведТов-ХарактерТов" СортТов="СортТов" СерияТов="ДопСведТов-СерияТов" АртикулТов="ДопСведТов-АртикулТов" КодТов="ДопСведТов-КодТов" ГТИН="10000057074365" КодВидТов="1111111111">
							<НалУчАморт АмГруппа="12" КодОКОФ="165" СрПолИспОС="234" ФактСрокИсп="100" />
							<СумНалВосст>
								<СумНал>1345.00</СумНал>
							</СумНалВосст>
						</ДопСведТов>
						<Акциз>
							<БезАкциз>без акциза</БезАкциз>
						</Акциз>
						<СумНал>
							<СумНал>1000.00</СумНал>
						</СумНал>
					</СведТов>
					<ВсегоОпл СтТовБезНДСВсего="8965.00" СтТовУчНалВсего="10000.00">
						<СумНалВсего>
							<СумНал>456.00</СумНал>
						</СумНалВсего>
					</ВсегоОпл>
				</ТаблСчФакт>
				<СвПродПер>
					<СвПер СодОпер="СвПер-СодОпер" ВидОпер="СвПер-ВидОпер" ДатаПер="15.02.2020" ДатаНачПер="16.02.2020" ДатаОконПер="16.02.2021">
						<ОснПер РеквНаимДок="ОснПер-РеквНаимДок" РеквНомерДок="567" РеквДатаДок="14.02.2020">
							<РеквИдРекСост>
								<ИННФЛ>144647873819</ИННФЛ>
							</РеквИдРекСост>
						</ОснПер>
						<СвЛицПер>
							<ИнЛицо>
								<ПредОргПер Должность="ПредОргПер-Должность" НаимОргПер="ПредОргПер-НаимОргПер" ИныеСвед="ПредОргПер-ИныеСвед">
									<ОснДоверОргПер РеквНаимДок="ОснДоверОргПер-РеквНаимДок" РеквНомерДок="098" РеквДатаДок="03.02.2020">
										<РеквИдРекСост>
											ИННЮЛ>4620212891</ИННЮЛ>
										</РеквИдРекСост>
									</ОснДоверОргПер>
									<ОснПолнПредПер РеквНаимДок="ОснПолнПредПер-РеквНаимДок" РеквНомерДок="098" РеквДатаДок="03.02.2020">
										<РеквИдРекСост>
											<ИННЮЛ>4620212891</ИННЮЛ>
										</РеквИдРекСост>
									</ОснПолнПредПер>
									<ФИО Фамилия="Иванов" Имя="Иван" Отчество="Иванович" />
								</ПредОргПер>
							</ИнЛицо>
						</СвЛицПер>
						<СвПерВещи>
							<ДокПерВещ РеквНаимДок="ДокПерВещ-РеквНаимДок" РеквНомерДок="098" РеквДатаДок="03.02.2020">
								<РеквИдРекСост>
									<ИННЮЛ>4620212891</ИННЮЛ>
								</РеквИдРекСост>
							</ДокПерВещ>
						</СвПерВещи>
					</СвПер>
					<ИнфПолФХЖ3 ИдФайлИнфПол="9c3adc2b-a085-4acd-af8c-3494290d782c">
						<ТекстИнф Идентиф="Идентиф1в" Значен="Значен1в" />
						<ТекстИнф Идентиф="Идентиф2в" Значен="Значен2в" />
					</ИнфПолФХЖ3>
				</СвПродПер>
				<Подписант ТипПодпис="1" ДатаПодДок="21.01.2024" СпосПодтПолном="3" ДопСведПодп="Подписант-ДопСведПодп" Должн="Подписант-Должн">
					<ФИО Фамилия="Петров" Имя="Петр" Отчество="Петрович" />
					<СвДоверЭл НомДовер="4a743152-e772-4249-9a47-e2e290258e79" ДатаВыдДовер="17.09.2018" ВнНомДовер="123" ДатаВнРегДовер="18.09.2018" ИдСистХран="СвДоверЭл-ИдСистХран" УРЛСист="СвДоверЭл-УРЛСист" />
				</Подписант>
				<ОснДоверОргСост РеквНаимДок="ОснДоверОргСост-РеквНаимДок" РеквНомерДок="123" РеквДатаДок="01.02.2003">
					<РеквИдРекСост>
						<ДаннИно КодСтр="112" НаимСтран="Беларусь" Наим="ДаннИно-Наим" ИдСтат="ИГ" ИныеСвед="ДаннИно-ИныеСвед" Идентиф="ДаннИно-Идентиф" />
					</РеквИдРекСост>
				</ОснДоверОргСост>
			</Документ>
		</Файл>

Примеры для работы с другими форматами приведены на страницах:

	- :doc:`../howto/utd820`
	- :doc:`../howto/utd970`


Генерация последующих титулов
-----------------------------

Если тип документа предусматривает более одного титула, то нужно сгенерировать последующие титулы — т.е. титулы для ``titleIndex`` > 0.
Алгоритм генерации последующих титулов аналогичен генерации титула отправителя, за исключением дополнительных параметров в запросе.

В большинстве случаев в содержимом последующих титулов нужно указать информацию из предыдущих титулов, поэтому в запрос нужно передавать идентификаторы уже существующего в Диадоке документа: ``letterId`` и ``documentId``.


Генерация титула с настройкой редактирования
--------------------------------------------

Если при создании документа заданы :ref:`настройки редактирования <editing_settings>`, то валидация содержимого титула будет выполняться по XSD-схеме, соответствующей указанной настройке редактирования.

То есть если настройка редактирования позволяет не указывать какой-либо атрибут, то с помощью метода :doc:`../http/GenerateTitleXml` можно сгенерировать XML-файл, в котором этот атрибут будет отсутствовать. Валидация такого файла будет осуществляться так, как будто неуказанный атрибут является опциональным по XSD-схеме.


.. _generate_title_xml_poa:

Генерация титула с МЧД в подписанте
-----------------------------------

Большинство формализованных документов должны содержать в себе информацию о подписанте документа.

При подписании документа юридического лица сертификатом, выданным на физическое лицо, в блоке «Подписант» невозможно автоматически заполнить поля, которых нет в сертификате, — например, наименование организации, ИНН ЮЛ. В этом случае необходимо использовать :doc:`машиночитаемую доверенность <powerofattorney>` (МЧД).

Чтобы при генерации методом :doc:`../http/GenerateTitleXml` заполнить эти поля, укажите в теле запроса ``UserDataXml`` информацию о МЧД:

	- если детали подписанта задаются по сертификату блоком ``SignerReference``, то заполните блок ``PowerOfAttorney``: укажите регистрационный номер МЧД и ИНН доверителя или используйте МЧД по умолчанию  спомощью значения ``UseDefault``;
	- если детали подписанта задаются в явном виде с помощью блока ``SignerDetails``, то при формировании подписанта по МЧД самостоятельно определите необходимость использования ИНН подписанта и название организации для ЮЛ из МЧД.

**Блок PowerOfAttorney в XSD-схеме:**

.. container:: toggle

 .. code-block:: xml

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


**Пример тела запроса метода GenerateTitleXml (UserDataXml) для формата 820:**

.. container:: toggle

 .. code-block:: xml

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
				<OrganizationReference OrgType="1" BoxId="53d55d52-9317-4ad4-a7d9-5e9dd3cd6367"/>
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

**Пример тела ответа метода GenerateTitleXml:**

.. container:: toggle

 .. code-block:: xml

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


Генерация титула с МЧД в содержимом документа
---------------------------------------------

Для некоторых форматов документов можно передавать информацию о :doc:`машиночитаемой доверенности <powerofattorney>` (МЧД) в содержимом документа. Сейчас это следующие форматы:

	- акт сверки формата, утвержденного приказом `№ ЕД-7-26/405@ <https://normativ.kontur.ru/document?moduleId=1&documentId=425482>`_,
	- акт о приемке выполненных работ КС-2 формата, утвержденного приказом `№ ЕД-7-26/691@ <https://normativ.kontur.ru/document?moduleId=1&documentId=431929>`__,
	- документы формата, утвержденного приказом `№ ЕД-7-26/970@ <https://normativ.kontur.ru/document?moduleId=1&documentId=464695>`__.

Для генерации документа с МДЧ в содержимом заполните блок ``PowerOfAttorney`` в XSD-схеме универсального подписанта конкретного формата документа.

В структуре можно указать сведения об электронной (элемент ``Electronic``) или бумажной доверенности (элемент ``Paper``).
Электронную доверенность можно выбрать из хранилища Диадока (элемент ``Storage``) или указать данные вручную (элемент ``Manual``).
Если вы выбираете доверенность из хранилища, можно использовать МЧД сотрудника по умолчанию (атрибут ``UseDefault = 1``) или указать другую, заполнив регистрационный номер и ИНН доверителя внутри структуры ``FullId`` при одновременном значении атрибута ``UseDefault = 0``.

**Блок PowerOfAttorney в XSD-схеме для универсального подписанта Акта сверки 405 формата:**

.. container:: toggle

 .. code-block:: xml

	<xs:complexType name="PowerOfAttorney">
		<xs:sequence>
			<xs:element name="Electronic" type="Electronic" minOccurs="0">
				<xs:annotation>
					<xs:documentation>Электронная доверенность</xs:documentation>
				</xs:annotation>
			</xs:element>
			<xs:element name="Paper" type="Paper" minOccurs="0">
				<xs:annotation>
					<xs:documentation>Бумажная доверенности</xs:documentation>
				</xs:annotation>
			</xs:element>
		</xs:sequence>
	</xs:complexType>
	<xs:complexType name="Electronic">
		<xs:sequence>
			<xs:choice>
				<xs:element name="Storage" type="Storage">
					<xs:annotation>
						<xs:documentation>Автоматическое заполнение информации по доверенности на основе номера и ИНН</xs:documentation>
					</xs:annotation>
				</xs:element>
				<xs:element name="Manual" type="Manual">
					<xs:annotation>
						<xs:documentation>Ручное заполнение данных доверенности</xs:documentation>
					</xs:annotation>
				</xs:element>
			</xs:choice>
		</xs:sequence>
	</xs:complexType>
	<xs:complexType name="Storage">
		<xs:sequence>
			<xs:element name="FullId" minOccurs="0">
				<xs:complexType>
					<xs:attribute name="RegistrationNumber" type="guid" use="required">
						<xs:annotation>
							<xs:documentation>Номер доверенности</xs:documentation>
						</xs:annotation>
					</xs:attribute>
					<xs:attribute name="IssuerInn" type="inn" use="required">
						<xs:annotation>
							<xs:documentation>ИНН организации, выдавшей доверенность</xs:documentation>
						</xs:annotation>
					</xs:attribute>
				</xs:complexType>
			</xs:element>
		</xs:sequence>
		<xs:attribute name="UseDefault" use="required">
			<xs:annotation>
				<xs:documentation>Автоматическое заполнение информации на основе доверенности, используемой сотрудником по умолчанию</xs:documentation>
			</xs:annotation>
			<xs:simpleType>
				<xs:restriction base="xs:string">
					<xs:enumeration value="true" />
					<xs:enumeration value="false" />
				</xs:restriction>
			</xs:simpleType>
		</xs:attribute>
	</xs:complexType>
	<xs:complexType name="Manual">
		<xs:attribute name="RegistrationNumber" type="guid">
			<xs:annotation>
				<xs:documentation>Номер доверенности</xs:documentation>
			</xs:annotation>
		</xs:attribute>
		<xs:attribute name="RegistrationDate" type="date">
			<xs:annotation>
				<xs:documentation>Дата совершения (выдачи) доверенности</xs:documentation>
			</xs:annotation>
		</xs:attribute>
		<xs:attribute name="InternalNumber" type="string50">
			<xs:annotation>
				<xs:documentation>Внутренний регистрационный номер доверенности</xs:documentation>
			</xs:annotation>
		</xs:attribute>
		<xs:attribute name="InternalDate" type="date">
			<xs:annotation>
				<xs:documentation>Дата внутренней регистрации доверенности</xs:documentation>
			</xs:annotation>
		</xs:attribute>
		<xs:attribute name="SystemId" type="string500">
			<xs:annotation>
				<xs:documentation>Идентифицирующая информация об информационной системе, в которой осуществляется хранение доверенности</xs:documentation>
			</xs:annotation>
		</xs:attribute>
	</xs:complexType>
	<xs:complexType name="Paper">
		<xs:annotation>
			<xs:documentation>Сведения о доверенности, используемой для подтверждения полномочий на бумажном носителе</xs:documentation>
		</xs:annotation>
		<xs:sequence>
			<xs:element name="Person" type="Fio" minOccurs="0">
				<xs:annotation>
					<xs:documentation>Фамилия, имя, отчество (при наличии) лица, подписавшего доверенность</xs:documentation>
				</xs:annotation>
			</xs:element>
		</xs:sequence>
		<xs:attribute name="InternalNumber" type="string50">
			<xs:annotation>
				<xs:documentation>Внутренний регистрационный номер доверенности</xs:documentation>
			</xs:annotation>
		</xs:attribute>
		<xs:attribute name="RegistrationDate" type="date">
			<xs:annotation>
				<xs:documentation>Дата совершения (выдачи) доверенности</xs:documentation>
			</xs:annotation>
		</xs:attribute>
		<xs:attribute name="IssuerInfo" type="string1000">
			<xs:annotation>
				<xs:documentation>Сведения о доверителе</xs:documentation>
			</xs:annotation>
		</xs:attribute>
	</xs:complexType>


----

.. rubric:: См. также

*Инструкции:*
	- :doc:`powerofattorney`

*Методы для работы с титулами:*
	- :doc:`../http/GenerateTitleXml` — генерирует XML-файл любого титула для любого типа документа
	- :doc:`../http/ParseTitleXml` — парсит XML-файл титула на элементы