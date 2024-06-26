Работа с УПД в 820 и 970 форматах
=================================

.. contents:: :local:
	:depth: 3

До 1 апреля 2025 года можно использовать следующие форматы универсального передаточного документа (УПД):

	- Формат №820, утвержденный `приказом ФНС России от 19.12.2018 № ММВ-7-15/820@ <https://normativ.kontur.ru/document?moduleId=1&documentId=328588>`_,
	- Формат №970, утвержденный `приказом ФНС России от 19.12.2023 № ЕД-7-26/970@ <https://normativ.kontur.ru/document?moduleId=1&documentId=464695>`_.

После 1 апреля 2025 года можно будет использовать только формат №970.

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
		- ``documentFunction = СЧФ``,
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

			POST /GenerateTitleXml?boxId=74ef3a00-c625-4ef0-9b50-65bf7f96b9ae&documentTypeNamedId=UniversalTransferDocument&documentFunction=СЧФ&documentVersion=utd970_05_02_01&titleIndex=0 HTTP/1.1
			Host: diadoc-api.kontur.ru
			Authorization: DiadocAuth ddauth_api_client_id={{ключ разработчика}}, ddauth_token={{авторизационный токен}}
			Content-Type: application/xml; charset=utf-8

	.. tab:: УПД 820

		.. code-block:: http

			POST /GenerateTitleXml?boxId=a96be310-0982-461a-8b2a-91d198b7861c&documentTypeNamedId=UniversalTransferDocument&documentFunction=СЧФДОП&documentVersion=utd820_05_01_02_hyphen&titleIndex=0 HTTP/1.1
			Host: diadoc-api.kontur.ru
			Authorization: DiadocAuth ddauth_api_client_id={{ключ разработчика}}, ddauth_token={{авторизационный токен}}
			Content-Type: application/xml; charset=utf-8

**Пример тела запроса метода GenerateTitleXml (UserDataXml):**

.. tabs::

	.. tab:: УПД 970

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

	.. tab:: УПД 820

		.. container:: toggle

		 .. code-block:: xml

			<?xml version="1.0" encoding="utf-8"?>
			<UniversalTransferDocumentWithHyphens Function="СЧФДОП"
					DocumentDate="01.08.2019"
					DocumentNumber="140"
					DocumentCreator="1"
					DocumentCreatorBase="1"
					CircumFormatInvoice="4"
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

**Пример тела ответа метода GenerateTitleXml (титул продавца):**

.. tabs::

	.. tab:: УПД 970

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

	.. tab:: УПД 820

		.. container:: toggle

		 .. code-block:: xml

			HTTP/1.1 200 OK

			<?xml version="1.0" encoding="windows-1251"?>
			<Файл ИдФайл="ON_NSCHFDOPPR_2BM-9670670494-967001000-202201240241297341956_2BM-participantId1_20220124_f972e93e-4c69-4c9e-9656-be3a5a072e72" ВерсФорм="5.01" ВерсПрог="Diadoc 1.0">
				<СвУчДокОбор ИдОтпр="2BM-participantId1" ИдПол="2BM-9670670494-967001000-202201240241297341956">
					<СвОЭДОтпр ИННЮЛ="6663003127" ИдЭДО="2BM" НаимОрг="АО &quot;ПФ &quot;СКБ Контур&quot;" />
				</СвУчДокОбор>
				<Документ КНД="1115131" ВремИнфПр="18.17.45" ДатаИнфПр="24.01.2022" НаимЭконСубСост="1" Функция="СЧФДОП" ПоФактХЖ="Документ об отгрузке товаров (выполнении работ), передаче имущественных прав (документ об оказании услуг)" НаимДокОпр="Счет-фактура и документ об отгрузке товаров (выполнении работ), передаче имущественных прав (документ об оказании услуг)" ОснДоверОргСост="1">
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
					<ДопСвФХЖ1 НаимОКВ="Российский рубль" ОбстФормСЧФ="4" />
				</СвСчФакт>
				<ТаблСчФакт>
					<СведТов НомСтр="1" НаимТов="Товарная позиция" ОКЕИ_Тов="796" КолТов="0" ЦенаТов="0.00" СтТовБезНДС="0.00" НалСт="без НДС" СтТовУчНал="0.00">
						<Акциз>
							<СумАкциз>
								10.00
							</СумАкциз>
						</Акциз>
						<СумНал>
							<СумНал>
								0.00
							</СумНал>
						</СумНал>
						<ДопСведТов НаимЕдИзм="шт" />
					</СведТов>
					<ВсегоОпл СтТовБезНДСВсего="0.00" СтТовУчНалВсего="0.00">
						<СумНалВсего>
							<СумНал>
								0.00
							</СумНал>
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