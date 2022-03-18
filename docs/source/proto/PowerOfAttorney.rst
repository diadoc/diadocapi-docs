PowerOfAttorney
===============

Структура ``PowerOfAttorney`` предназначена для хранения информации о машиночитаемой доверенности (МЧД).

.. code-block:: protobuf

    message PowerOfAttorney {
        required PowerOfAttorneyFullId FullId = 1;
        required PowerOfAttorneyIssuer Issuer = 2;
        required PowerOfAttorneyConfidant Confidant = 3;
        required Timestamp StartAt = 4;
        required Timestamp ExpireAt = 5;
    }

    message PowerOfAttorneyIssuer {
        optional PowerOfAttorneyIssuerType Type = 1 [default = UnknownIssuerType];
        optional PowerOfAttorneyIssuerLegalEntity LegalEntity = 2;
        optional PowerOfAttorneyIssuerForeignEntity ForeignEntity = 3;
        optional PowerOfAttorneyIssuerIndividualEntity IndividualEntity = 4;
        optional PowerOfAttorneyIssuerPhysicalEntity PhysicalEntity = 5;
    }

    enum PowerOfAttorneyIssuerType {
        UnknownIssuerType = 0;
        LegalEntity = 1;
        ForeignEntity = 2;
        IndividualEntity = 3;
        PhysicalEntity = 4;
    }

    message PowerOfAttorneyIssuerLegalEntity {
        required string Inn = 1;
        required string Kpp = 2;
        required string OrganizationName = 3;
    }

    message PowerOfAttorneyIssuerForeignEntity {
        optional string Inn = 1;
        optional string Kpp = 2;
        required string OrganizationName = 3;
    }

    message PowerOfAttorneyIssuerIndividualEntity {
        required string Inn = 1;
        required string OrganizationName = 3;
    }

    message PowerOfAttorneyIssuerPhysicalEntity {
        required string Inn = 1;
        optional FullName PersonName = 2;
    }

    message PowerOfAttorneyConfidant {
        required FullName PersonName = 1;
        required string Inn = 2;
        optional PowerOfAttorneyConfidantOrganization Organization = 3;
    }

    message PowerOfAttorneyConfidantOrganization {
        required string Inn = 1;
        optional string Kpp = 2;
        required string Name = 3;
    }
   
- ``FullId`` — идентификатор МЧД, представленный структурой :doc:`PowerOfAttorneyFullId`.
- ``Issuer`` — данные о доверителе, представленные структурой ``PowerOfAttorneyIssuer`` с полями:

	- ``Type`` — тип доверителя, принимает значения из перечисления ``PowerOfAttorneyIssuerType``:
	
		- ``LegalEntity`` — юридическое лицо;
		- ``ForeignEntity`` — иностранная организация;
		- ``IndividualEntity`` — индивидуальный предприниматель;
		- ``PhysicalEntity`` — физическое лицо.
		
	- ``LegalEntity`` — данные о юридическом лице. Используются в случае, если тип доверителя имеет значение ``Type=LegalEntity``. Представлены структурой ``PowerOfAttorneyIssuerLegalEntity`` с полями:
	
		- ``Inn`` — ИНН доверителя.
		- ``Kpp`` — КПП доверителя.
		- ``OrganizationName`` — наименование организации.
		
	- ``ForeignEntity`` — данные об иностранной организации. Используются в случае, если тип доверителя имеет значение ``Type=ForeignEntity``. Представлены структурой ``PowerOfAttorneyIssuerForeignEntity`` с полями:
	
		- ``Inn`` — ИНН доверителя.
		- ``Kpp`` — КПП доверителя.
		- ``OrganizationName`` — наименование организации.

	- ``IndividualEntity`` — данные об индивидуальном предпринимателе. Используются в случае, если тип доверителя имеет значение ``Type=IndividualEntity``. Представлены структурой ``PowerOfAttorneyIssuerIndividualEntity`` с полями:
	
		- ``Inn`` — ИНН доверителя.
		- ``OrganizationName`` — Наименование индивидуального предпринимателя.

	- ``PhysicalEntity`` — данные о физическом лице. Используются в случае, если тип доверителя имеет значение ``Type=PhysicalEntity``. Представлены структурой ``PowerOfAttorneyIssuerPhysicalEntity`` с полями:
	
		- ``Inn`` — ИНН доверителя.
		- ``PersonName`` — ФИО доверителя.
	
- ``Confidant`` — данные о представителе, представленные структурой ``PowerOfAttorneyConfidant`` с полями:

	- ``PersonName`` — ФИО представителя.
	- ``Inn`` — ИНН представителя: физического или юридического лица. В случае юридического лица используется ИНН уполномоченного представителя этой организации, который может действовать без доверенности.
	- ``Organization`` — данные об организации. Используются в случае, если представителем является организация. Представлены структурой ``PowerOfAttorneyConfidantOrganization`` с полями:
	
		- ``Inn`` — ИНН доверителя.
		- ``Kpp`` — КПП доверителя.
		- ``Name`` — наименование организации.

- ``StartAt`` — дата начала действия МЧД, представленная структурой :doc:`Timestamp`.
- ``ExpireAt`` — срок действия МЧД, представленный структурой :doc:`Timestamp`.

----

.. rubric:: Использование

Структура ``PowerOfAttorney`` используется:

- в структуре :doc:`PowerOfAttorneyRegisterResult`
- в структуре :doc:`EmployeePowerOfAttorney`
- в теле ответа метода :doc:`../http/GetPowerOfAttorneyInfo`