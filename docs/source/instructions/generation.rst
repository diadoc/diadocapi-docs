Генерация формализованного документа
====================================

.. contents:: :local:
	:depth: 3

Через Диадок можно отправить как формализованные, так и неформализованные документы. Неформализованные документы могут быть представлены в любом формате. Формализованные документы должны соответствовать форматам, рекомендованному ФНС.

Формализованный документ, в зависимости от формата и функции, может состоять из одного или нескольких титулов. Каждый титул представляет собой XML-файл, соответствующий установленной ФНС XSD-схеме. 

Вы можете подготовить XML-файл титула двумя способами:

	- сформировать титул самостоятельно, заполнив данными весь XML-файл титула в соответствии с XSD-схемой;
	- воспользоваться методом API :doc:`../http/GenerateTitleXml`, чтобы сгенерировать титул, заполнив только некоторые данные.


Принцип работы метода генерации
-------------------------------

Некоторые данные в титуле может заполнить только пользователь — это информация о товарах, услугах и т.д. Остальные данные Диадок может заполнить автоматически на основании формата документа и информации в системе, — например, реквизиты организации продавца и покупателя по идентификатору ящика, значения КНД, версии формата, версии программы и т.д.

Чтобы упростить процесс заполнения данных для пользователя, Диадок позволяет заполнить только ту часть XML-файла титула, которая содержит пользовательские данные, — упрощенный XML-файл UserDataXml. На его основе метод генерации ``GenerateTitleXml`` сформирует титул, автоматически дополнив его всеми необходимыми данными согласно XSD-схеме.

Чтобы сформировать упрощенный XML-файл UserDataXml, нужно использовать не полную XSD-схему, а упрощенную — UserDataXsd. Она содержит информацию для генерации пользовательской части титула. Получить UserDataXsd можно с помощью метода :doc:`../http/GetDocumentTypes`.

Схема работы метода ``GenerateTitleXml``:

.. image:: ../_static/img/diadoc-api-generate-xml-schema1.png
	:align: center

Чтобы сгенерировать документ методом ``GenerateTitleXml``, помимо UserDataXml нужно передать в метод следующие параметры:

	- ``documentTypeNamedId`` — тип документа;
	- ``documentFunction`` — функция документа;
	- ``documentVersion`` — версия документа;
	- ``titleIndex`` — идентификатор титула документа, т.е. порядковый номер титула, пронумерованный с ``0``;

Получить все эти значения можно с помощью метода :doc:`../http/GetDocumentTypes`. Инструкция о получении данных для титула из метода ``GetDocumentTypes`` приведена в разделе :ref:`doctype_title`.

Метод ``GenerateTitleXml`` вернет в ответе XML-файл титула, сгенерированный в соответствии с XSD-схемой. Дальше полученный файл можно:

	- :doc:`подготовить к подписанию <preparetosign>`, подписать и :ref:`отправить <doc_send>`,
	- :ref:`сохранить и отправить позже <doc_delaysend>`,
	- :ref:`сохранить как черновик <doc_draft>`.

.. note::
	Ниже в качестве примеров используются УПД формата приказа ФНС № 970 и 820, но описанный алгоритм применим и к другим форматам документов.


.. _generate_sender_title:

Генерация титула отправителя
----------------------------

Алгоритм для генерации титула отправителя выглядит следующим образом.

#. Получение данных о типе документа.

   На этом этапе нужно получить данные об интересующем нас типе документа с помощью метода :doc:`../http/GetDocumentTypes`. Инструкция о получении данных для титула из метода ``GetDocumentTypes`` приведена в разделе :ref:`doctype_title`.

   Из ответа метода ``GetDocumentTypes`` для УПД возьмем следующие значения для параметров метода ``GenerateTitleXml``:

   .. tabs::

      .. tab:: УПД 970

         .. include:: ../include/generate_utd970_05_02_01_title0_params.txt

      .. tab:: УПД 820

         .. include:: ../include/generate_utd820_05_01_02_hyphen_title0_params.txt

   Кроме этого получаем значение поля ``UserDataXsdUrl`` — ссылку для получения XSD-схемы упрощенного XML-фала титула:

   .. tabs::

      .. tab:: УПД 970

         ``/GetContent?typeNamedId=UniversalTransferDocument&function=СЧФДОП&version=utd970_05_02_01&titleIndex=0&contentType=UserContractXsd``

      .. tab:: УПД 820

         ``/GetContent?typeNamedId=UniversalTransferDocument&function=СЧФДОП&version=utd820_05_01_02_hyphen&titleIndex=0&contentType=UserContractXsd``

   Вызвав метод ``GetContent`` по указанной ссылке, получим упрощенную схему UserDataXsd.

#. Подготовка содержимого титула.

   Для метода генерации нужно подготовить упрощенный XML-файл титула — UserDataXml, соответствующей полученной на предыдущем этапе схеме UserDataXsd.
   
   Как сформировать UserDataXml — решает разработчик интеграционного решения. Один из вариантов — это кодогенерация XML на основе упрощенной XSD-схемы титула. 

   В C# SDK для всех версий форматов приказов №820 и №970 есть `пример кодогенерации <https://github.com/diadoc/diadocsdk-csharp/tree/master/src/DataXml>`_ титулов.
   Кодогенерация осуществляется `инструментом xsd.exe <https://docs.microsoft.com/ru-ru/dotnet/standard/serialization/xml-schema-definition-tool-xsd-exe>`_.
   Чтобы воспользоваться ей в C#-клиенте, нужно заполнить объект ``UniversalTransferDocument`` для титула отправителя или ``UniversalTransferDocumentBuyerTitle`` для титула получателя и `сериализовать его в XML <https://github.com/diadoc/diadocsdk-csharp/blob/master/src/XmlSerializerExtensions.cs>`_.

#. Генерация титула.

   Титул генерируется с помощью метода :doc:`../http/GenerateTitleXml`. В него нужно передать полученные на предыдущих этапах параметры: тип, функцию, версию, порядковый номер титула и содержимое UserDataXml.

   Тело ответа, полученное в результате выполнения метода, содержит XML-файл первого титула документа.

   **Пример HTTP-запроса метода GenerateTitleXml:**

   .. tabs::

      .. tab:: УПД 970

         .. literalinclude:: ../include/generate_utd970_05_02_01_title0_query.txt

      .. tab:: УПД 820

         .. literalinclude:: ../include/generate_utd820_05_01_02_hyphen_title0_query.txt

   **Пример тела запроса метода GenerateTitleXml (UserDataXml):**

   .. tabs::

      .. tab:: УПД 970

         .. container:: toggle

            .. literalinclude:: ../include/generate_utd970_05_02_01_title0_body.xml

      .. tab:: УПД 820

         .. container:: toggle

            .. literalinclude:: ../include/generate_utd820_05_01_02_hyphen_title0_body.xml

   **Пример тела ответа метода GenerateTitleXml (титул отправителя):**

   .. tabs::

      .. tab:: УПД 970

         .. container:: toggle

            .. literalinclude:: ../include/generate_utd970_05_02_01_title0_resp.xml
               :encoding: windows-1251

      .. tab:: УПД 820

         .. container:: toggle

            .. literalinclude:: ../include/generate_utd820_05_01_02_hyphen_title0_resp.xml
               :encoding: windows-1251


Генерация последующих титулов
-----------------------------

Если тип документа предусматривает более одного титула, то нужно сгенерировать последующие титулы — т.е. титулы для ``titleIndex`` > 0.

Алгоритм генерации последующих титулов аналогичен генерации титула отправителя. Различие будет только в дополнительных параметрах ``letterId`` и ``documentId`` запроса, т.к. в большинстве случаев в содержимом последующих титулов нужно указать информацию из предыдущих титулов.

Чтобы сгенерировать титул покупателя для УПД формата приказа ФНС № 970 и 820, нужно получить необходимую информацию из метода :doc:`../http/GetDocumentTypes`. Инструкция о получении данных для титула из метода ``GetDocumentTypes`` приведена в разделе :ref:`doctype_title`.

Из ответа метода ``GetDocumentTypes`` для УПД возьмем те же значения для параметров метода ``GenerateTitleXml``, что и для титула продавца, но номер титула будет другой:

.. tabs::

	.. tab:: УПД 970

		.. include:: ../include/generate_utd970_05_02_01_title1_params.txt

	.. tab:: УПД 820

		.. include:: ../include/generate_utd820_05_01_02_hyphen_title1_params.txt

Кроме этого нужно подготовить содержимое титула — упрощенный XML-файл UserDataXml. С помощью полученных данных можно сгенерировать титул покупателя.

**Пример HTTP-запроса метода GenerateTitleXml:**

.. tabs::

	.. tab:: УПД 970

		.. literalinclude:: ../include/generate_utd970_05_02_01_title1_query.txt

	.. tab:: УПД 820

		.. literalinclude:: ../include/generate_utd820_05_01_02_hyphen_title1_query.txt

**Пример тела запроса метода GenerateTitleXml (UserDataXml):**

.. tabs::

	.. tab:: УПД 970

		.. container:: toggle

			.. literalinclude:: ../include/generate_utd970_05_02_01_title1_body.xml

	.. tab:: УПД 820

		.. container:: toggle

			.. literalinclude:: ../include/generate_utd820_05_01_02_hyphen_title1_body.xml

**Пример тела ответа метода GenerateTitleXml (титул покупателя):**

.. tabs::

	.. tab:: УПД 970

		.. container:: toggle

			.. literalinclude:: ../include/generate_utd970_05_02_01_title1_resp.xml
				:encoding: windows-1251

	.. tab:: УПД 820

		.. container:: toggle

			.. literalinclude:: ../include/generate_utd820_05_01_02_hyphen_title1_resp.xml
				:encoding: windows-1251


Генерация титула с настройкой редактирования
--------------------------------------------

Если при создании документа заданы :doc:`настройки редактирования <editingsettings>`, то валидация содержимого титула будет выполняться по XSD-схеме, соответствующей указанной настройке редактирования.

То есть если настройка редактирования позволяет не указывать какой-либо атрибут, то с помощью метода :doc:`../http/GenerateTitleXml` можно сгенерировать XML-файл, в котором этот атрибут будет отсутствовать. Валидация такого файла будет осуществляться так, как будто неуказанный атрибут является опциональным по XSD-схеме.

XSD-схемы для каждой настройки редактирования приведены в разделе :doc:`editingsettings`.

Кроме XSD-схемы генерация титула с настройкой редактирования ничем не отличается от обычного титула и производится по тому же алгоритму.


.. _generate_title_tracing:

Генерация титула с прослеживаемыми товарами
-------------------------------------------

Чтобы указать в титуле :doc:`прослеживаемые товары <../howto/tracing>`, заполните в UserDataXml блок ``ItemTracingInfos`` элементами ``ItemTracingInfo``:

	- ``RegNumberUnit`` — регистрационный номер партии товаров [`НомТовПрослеж <https://normativ.kontur.ru/document?moduleId=1&documentId=328588&rangeId=239773>`__];
	- ``Unit`` — единица количественного учета товара, используемая в целях осуществления прослеживаемости [`ЕдИзмПрослеж <https://normativ.kontur.ru/document?moduleId=1&documentId=328588&rangeId=239774>`__];
	- ``UnitName`` — наименование единицы количественного учета товара, используемой в целях осуществления прослеживаемости [`НаимЕдИзмПрослеж <https://normativ.kontur.ru/document?moduleId=1&documentId=328588&rangeId=239775>`__];
	- ``Quantity`` — количество товара в единицах измерения прослеживаемого товара [`КолВЕдПрослеж <https://normativ.kontur.ru/document?moduleId=1&documentId=328588&rangeId=239776>`__];
	- ``ItemAddInfo`` — дополнительный показатель для идентификации товаров, подлежащих прослеживаемости [`ДопИнфПрослеж <https://normativ.kontur.ru/document?moduleId=1&documentId=328588&rangeId=239777>`__];
	- ``PriceWithVatExcluded`` — стоимость товара, подлежащего прослеживаемости, без налога на добавленную стоимость, в рублях [`СтТовБезНДСПрослеж <https://normativ.kontur.ru/document?moduleId=1&documentId=464695&rangeId=6488112>`__] — обязательный параметр для УПД 970 формата.

Кроме дополнительных данных в UserDataXml генерация титула с прослеживаемыми товарами ничем не отличается от обычного титула и производится по тому же алгоритму.

Пример UserDataXml с прослеживаемыми товарами приведен в разделе :ref:`generate_sender_title`.


.. _generate_title_xml_poa:

Генерация титула с МЧД в подписанте
-----------------------------------

Большинство формализованных документов должны содержать в себе информацию о подписанте документа.

При подписании документа юридического лица сертификатом, выданным на физическое лицо, в блоке «Подписант» невозможно автоматически заполнить поля, которых нет в сертификате, — например, наименование организации, ИНН ЮЛ. В этом случае необходимо использовать :doc:`машиночитаемую доверенность <powerofattorney>` (МЧД).

Чтобы при генерации методом :doc:`../http/GenerateTitleXml` заполнить эти поля, укажите в теле запроса UserDataXml информацию о МЧД:

	- если детали подписанта задаются по сертификату блоком ``SignerReference``, то заполните блок ``PowerOfAttorney``: укажите регистрационный номер МЧД и ИНН доверителя или используйте МЧД по умолчанию с помощью значения ``UseDefault``;
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


**Пример тела запроса метода GenerateTitleXml (UserDataXml) для УПД формата 820:**

.. container:: toggle

 .. code-block:: xml

    <?xml version="1.0" encoding="utf-8"?>
    <UniversalTransferDocumentWithHyphens Function="СЧФ" DocumentDate="01.08.2019" DocumentNumber="140" DocumentCreator="1" DocumentCreatorBase="1" CircumFormatInvoice="1" Currency="643" >
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
                            <OrganizationReference OrgType="1" BoxId="1f208d03-2a60-4f64-91b1-b7aad54cfaf3"/>
                    </Buyer>
            </Buyers>
            <Table TotalWithVatExcluded="0" Vat="0" Total="0">
                <Item Product="Товарная позиция" Unit="796" Quantity="0" Price="0" TaxRate="без НДС" SubtotalWithVatExcluded="0" Vat="0" Subtotal="0" Excise="10"/>
            </Table>
            <TransferInfo OperationInfo="Товары переданы"/>
            <Signers>
                <SignerReference BoxId="09ae254c-5cd0-4082-84de-7ccb46d86f82" CertificateThumbprint="dec5fe8a9g83e11b04de55c1eb272ba2f36e655a">
                    <PowerOfAttorney UseDefault="false">
                        <FullId RegistrationNumber="c8a8949a-4907-4c36-9f48-7efb2fba1382" IssuerInn="3812125023" />
                    </PowerOfAttorney>
                </SignerReference>
            </Signers>
    </UniversalTransferDocumentWithHyphens>

**Пример тела ответа метода GenerateTitleXml:**

.. container:: toggle

 .. code-block:: xml

  HTTP/1.1 200 OK

    <?xml version="1.0" encoding="windows-1251"?>
    <Файл ИдФайл="ON_NSCHFDOPPR_2BM-9147414342-757645784-202407101104400484330_2BM-participantId1_20240711_bb56a59f-f6da-4079-b195-d08225ec9001" ВерсФорм="5.01" ВерсПрог="Diadoc 1.0">
        <СвУчДокОбор ИдОтпр="2BM-participantId1" ИдПол="2BM-9147414342-757645784-202407101104400484330">
            <СвОЭДОтпр ИННЮЛ="6663003127" ИдЭДО="2BM" НаимОрг="АО &quot;ПФ &quot;СКБ Контур&quot;" />
        </СвУчДокОбор>
        <Документ КНД="1115131" ВремИнфПр="07.34.25" ДатаИнфПр="11.07.2024" НаимЭконСубСост="1" Функция="СЧФ" ОснДоверОргСост="1">
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
                        <СвЮЛУч НаимОрг="Организация-получатель" ИННЮЛ="9147414342" КПП="757645784" />
                    </ИдСв>
                    <Адрес>
                        <АдрРФ Индекс="620142" КодРегион="66" Город="Екатеринбург" Улица="Сажинская" Дом="11" />
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
                <ЮЛ ИННЮЛ="3812125023" Должн="Работник" НаимОрг="ООО &quot;Еноты&quot;">
                    <ФИО Фамилия="Иванов" Имя="Петр" Отчество="Сергеевич" />
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
	- :doc:`utd`
	- :doc:`preparetosign`
	- :doc:`../howto/tracing`
	- :doc:`powerofattorney`

*Методы для работы с титулами:*
	- :doc:`../http/GenerateTitleXml` — генерирует XML-файл любого титула для любого типа документа
	- :doc:`../http/ParseTitleXml` — парсит XML-файл титула на элементы