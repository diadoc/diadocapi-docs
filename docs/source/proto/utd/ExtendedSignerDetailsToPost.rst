ExtendedSignerDetailsToPost
===========================

Структура ``ExtendedSignerToPost`` предназначена для записи информации о подписанте в базу данных.

.. code-block:: protobuf

     message ExtendedSignerToPost {
         optional string JobTitle = 1;
         optional string RegistrationCertificate = 2;
         required SignerType SignerType = 3 [default = LegalEntity];
         optional string SignerInfo = 4;
         required SignerPowers SignerPowers = 5;
         required SignerStatus SignerStatus = 6;
         optional string SignerPowersBase = 7;
         optional string SignerOrgPowersBase = 8;
      }

     enum SignerType {
         LegalEntity = 1;
         IndividualEntity = 2;
         PhysicalPerson = 3;
      }

     enum SignerPowers {
         InvoiceSigner = 0;
         PersonMadeOperation = 1;
         MadeAndSignOperation = 2;
         PersonDocumentedOperation = 3;
         MadeOperationAndSignedInvoice = 4;
         MadeAndResponsibleForOperationAndSignedInvoice = 5;
         ResponsibleForOperationAndSignerForInvoice = 6;
         ChairmanCommission = 7;
         MemberCommission = 8;
         PersonApprovedDocument = 21;
         PersonConfirmedDocument = 22;
         PersonAgreedOnDocument = 23;
         PersonOtherPower = 29;
     }

     enum SignerStatus {
        SellerEmployee = 1;
        InformationCreatorEmployee = 2;
        OtherOrganizationEmployee = 3;
        AuthorizedPerson= 4;
        BuyerEmployee = 5;
        InformationCreatorBuyerEmployee = 6;
    }

- ``JobTitle`` — должность подписанта.
- ``RegistrationCertificate`` — реквизиты свидетельства о регистрации индивидуального предпринимателя.
- ``SignerType`` — тип подписанта. Необязательное поле. По умолчанию принимает значение ``LegalEntity``. Принимает значения из перечисления ``SignerType``:

	- ``LegalEntity`` — представитель юридического лица;
	- ``IndividualEntity`` — индивидуальный предприниматель;
	- ``PhysicalPerson`` — физическое лицо.

- ``SignerInfo`` — иные сведения, идентифицирующие подписанта.

- ``SignerPowers`` — область полномочий подписанта, принимает значения из перечисления ``SignerPowers``:

	- ``InvoiceSigner`` — лицо, ответственное за подписание счетов-фактур;
	- ``PersonMadeOperation`` — лицо, совершившее сделку, операцию;
	- ``MadeAndSignOperation`` — лицо, совершившее сделку, операцию и ответственное за её оформление;
	- ``PersonDocumentedOperation`` — лицо, ответственное за оформление свершившегося события;
	- ``MadeOperationAndSignedInvoice`` — лицо, совершившее сделку, операцию и ответственное за подписание счетов-фактур;
	- ``MadeAndResponsibleForOperationAndSignedInvoice`` — лицо, совершившее сделку, операцию и ответственное за её оформление и за подписание счетов-фактур;
	- ``ResponsibleForOperationAndSignerForInvoice`` — лицо, ответственное за оформление свершившегося события и за подписание счетов-фактур;
	- ``ChairmanCommission`` — председатель комиссии;
	- ``MemberCommission`` — член комиссии;
	- ``PersonApprovedDocument`` — лицо, в полномочия которого входит утверждение документа, оформляющего событие (факт хозяйственной жизни);
	- ``PersonConfirmedDocument`` — лицо, в полномочия которого входит подтверждение оформленного события (факта хозяйственной жизни);
	- ``PersonAgreedOnDocument``— лицо, в полномочия которого входит согласование документа, оформляющего событие (факт хозяйственной жизни);
	- ``PersonOtherPower`` — лицо с иными полномочиями.

- ``SignerStatus`` — статус подписанта. Принимает значения из перечисления ``SignerStatus``:

	- ``SellerEmployee`` — работник организации — продавца товаров, работ, услуг, имущественных прав;
	- ``InformationCreatorEmployee`` — работник организации — составителя информации продавца;
	- ``OtherOrganizationEmployee`` — работник иной уполномоченной организации;
	- ``AuthorizedPerson`` — уполномоченное физическое лицо, в том числе индивидуальный предприниматель;
	- ``BuyerEmployee`` — работник организации — покупателя. Используется для документов в формате приказа №820;
	- ``InformationCreatorBuyerEmployee`` — работник организации — составителя файла обмена информации покупателя, если составитель файла обмена информации покупателя не является покупателем. Используется для документов в формате приказов №820 и №423.

- ``SignerPowersBase`` — основания полномочий подписанта. Обязательно, если ``SignerStatus = 4``.

- ``SignerOrgPowersBase`` — основания полномочий организации. Обязательно, если ``SignerStatus = 3``.
