Подготовка документа к подписанию
=================================

.. contents:: :local:
	:depth: 3


Метод :doc:`../http/PrepareDocumentsToSign` позволяет автоматически добавить в XML-файл информацию о подписанте. К подписанию можно подготовить :doc:`черновик<../entities/draft>`, незагруженный в Диадок формализованный документ или :ref:`неотправленный исходящий документ<doc_delaysend>`. Дополнить можно только первый титул документа, второй титул генерируется сразу со всеми данными. 

Кроме данных подписанта в файл можно добавить:

	- версию формата и программы,
	- дату и время формирования файлов,
	- идентификатор файла.

Данные подписанта, в зависимости от его типа, можно указать в структурах :doc:`../proto/Signer` или :doc:`../proto/ExtendedSigner` или в поле ``SignerContent``. Чтобы определить тип подписанта, используйте метод :doc:`../http/GetDocumentTypes`, тип подписанта вернется в поле ``SignerType`` структуры :ref:`SignerInfoV2`.

В зависимости от типа подписанта заполните его следующим образом:

	- простой подписант — при вызове метода ``PrepareDocumentsToSign`` заполните структуру ``Signer``.
	- расширенный подписант — при вызове метода ``PrepareDocumentsToSign`` заполните структуру ``ExtendedSigner``.
	- универсальный подписант — передайте бинарное представление упрощенного XML-файла подписанта в поле ``SignerContent``. Чтобы подготовить упрощенный XML-файл подписанта, выполните следующие действия: 

		#. Получите файл XSD-схемы упрощенного XML подписанта с помощью метода :doc:`../http/GetDocumentTypes`. Инструкция о получении данных для подписанта из метода ``GetDocumentTypes`` приведена в разделе :ref:`doctype_signer`.
		#. По полученной схеме подготовьте упрощенный XML-файл подписанта одним из следующих способов:

			- Используйте кодогенерацию в SDK. В C# SDK для всех версий формата 970 есть `пример кодогенерации <https://github.com/diadoc/diadocsdk-csharp/tree/master/src/DataXml/Utd970/V050201>`_ для подписанта. Кодогенерация осуществляется `инструментом xsd.exe <https://docs.microsoft.com/ru-ru/dotnet/standard/serialization/xml-schema-definition-tool-xsd-exe>`_. Чтобы воспользоваться ей в C#-клиенте, нужно заполнить объект ``Signer`` и `сериализовать его в XML <https://github.com/diadoc/diadocsdk-csharp/blob/master/src/XmlSerializerExtensions.cs>`_.
			- Укажите все данные для блока Подписант вручную в упрощенном XML-файле.
			- Укажите в файле данные, по которым Диадок сможет дополнить информацию, например, идентификатор ящика организации, отпечаток сертификата, регистрационный номер МЧД и ИНН доверителя. Диадок по переданным данным заполнит блок Подписант.

В ответе метод ``PrepareDocumentsToSign`` возвращает список документов, подготовленных к подписанию и отправке.

Пример сформированного в соответствии с :download:`XSD-схемой <../xsd/UniversalSignerForPatch.xsd>` подписанта для УПД 970 формата:

::

    <?xml version="1.0" encoding="Windows-1251"?>
    <Signers>
        <Signer SignatureType="1" SignerPowersConfirmationMethod="3" SigningDate="21.01.2024">
            <Certificate CertificateThumbprint="0e097989b91332008c052b5da5a7dd6424e6c2ac"/>
            <Fio FirstName="Петр" LastName="Петров" MiddleName="Петрович"/>
            <Position PositionSource="Manual">Подписант-Должн</Position>
            <SignerAdditionalInfo SignerAdditionalInfoSource="Manual">Подписант-ДопСведПодп</SignerAdditionalInfo>
            <PowerOfAttorney>
            <Electronic>
                <Manual RegistrationNumber="4a743152-e772-4249-9a47-e2e290258e79" RegistrationDate="17.09.2018" InternalNumber="123" InternalDate="18.09.2018" SystemId="СвДоверЭл-ИдСистХран" SystemUrl="СвДоверЭл-УРЛСист"/>
            </Electronic>
            </PowerOfAttorney>
        </Signer>
    </Signers>

- ``SignerStatus`` — статус подписанта, может принимать значения:

	- 1 — лицо, имеющее полномочия на подписание документа без доверенности,
	- 2 — лицо, имеющее полномочия на подписание документа на основании доверенности в электронной форме,
	- 3 — лицо, имеющее полномочия на подписание документа на основании доверенности на бумажном носителе.

- ``SignatureType`` — тип подписи, может принимать значения:

	- 1 — усиленная квалифицированная электронная подпись,
	- 2 — простая электронная подпись,
	- 3 — усиленная неквалифицированная электронная подпись.

- ``SignerPowersConfirmationMethod`` — способ подтверждения полномочий представителя на подписание документа. Используется для документов формата №970. Может принимать значения:

	- 1 — в соответствии с данными, содержащимися в электронной подписи,
	- 2 — в соответствии с доверенностью в электронной форме в машиночитаемом виде, если представление доверенности осуществляется посредством включения в каждый пакет электронных документов, подписываемых представителем,
	- 3 — в соответствии с доверенностью в электронной форме в машиночитаемом виде, если представление доверенности осуществляется из информационной системы. При этом необходимая информация для запроса доверенности из информационной системы, указана в электронном документе,
	- 4 — в соответствии с доверенностью в электронной форме в машиночитаемом виде, если представление доверенности осуществляется из информационной системы. При этом необходимая информация для запроса доверенности из информационной системы, представляется способом, отличным от указания в электронном документе,
	- 5 — в соответствии с доверенностью в форме документа на бумажном носителе,
	- 6 — иное.

- ``SigningDate`` — дата подписания документа.
- ``Certificate`` — данные сертификата подписанта. Обязательное поле. Можно передать:

	- ``CertificateThumbprint`` — отпечаток сертификата,
	- ``CertificateBytes`` — сертификат, сериализованный в массив байтов в DER-кодировке.

- ``Position`` — должность подписанта.
- ``PositionSource`` — способ заполнения должности сотрудника:

	- ``Employee`` — заполнение из данных сотрудника в Диадоке,
	- ``Certificate`` — заполнение из данных в сертификате,
	- ``StorageByTitleTypeId`` — заполнение из данных, сохраненных с помощью метода :doc:`../http/ExtendedSignerDetailsV2` для указанного сертификата и ``documentTitleType``,
	- ``Manual`` — ручное заполнение данных.

- ``SignerAdditionalInfo`` — дополнительные сведения о подписанте.
- ``SignerAdditionalInfoSource`` — способ заполнения дополнительных сведений, может принимать значения:

	- ``StorageByTitleTypeId`` — заполнение из данных, сохраненных с помощью метода :doc:`../http/ExtendedSignerDetailsV2` для указанного сертификата и ``documentTitleType``,
	- ``Manual`` — ручное заполнение данных.

- ``PowerOfAttorney`` — сведения о машиночитаемой доверенности. Доверенность может быть электронной или бумажной.

	- ``Electronic`` — электронная доверенность. Данные доверенности можно заполнить автоматически или вручную.

		- ``MethodOfProviding`` — способ представления доверенности. Обязательное поле. Может принимать значения:

			- 1 — представление доверенности осуществляется посредством ее включения в пакет электронных документов,
			- 2 — представление доверенности способом, не предусматривающим его включение в пакет электронных документов.

		- ``Storage`` — автоматическое заполнение информации по доверенности на основе номера и ИНН:

			- ``RegistrationNumber`` — номер доверенности, обязательное поле,
			- ``IssuerInn`` — ИНН организации, выдавшей доверенность, обязательное поле,
			- ``UseDefault`` — флаг, указывающий, нужно ли автоматически заполнить информацию на основе доверенности, используемой сотрудником по умолчанию. Обязательное поле.

		- ``Manual`` — ручное заполнение данных доверенности. Можно указать следующие данные:

			- ``RegistrationNumber`` — номер доверенности,
			- ``RegistrationDate`` — дата совершения (выдачи) доверенности,
			- ``InternalNumber`` — внутренний регистрационный номер доверенности,
			- ``InternalDate`` — дата внутренней регистрации доверенности,
			- ``SystemId`` — идентифицирующая информация об информационной системе, в которой осуществляется хранение доверенности.

	- ``Paper`` — бумажная доверенность. Можно указать следующие данные:

		- ``Fio`` — фамилия, имя, отчество (при наличии) лица, подписавшего доверенность,
		- ``InternalNumber`` — внутренний регистрационный номер доверенности, обязательное поле,
		- ``RegistrationDate`` — дата совершения (выдачи) доверенности, обязательное поле,
		- ``IssuerInfo`` — сведения о доверителе.
