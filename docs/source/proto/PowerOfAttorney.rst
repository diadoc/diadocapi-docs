PowerOfAttorney
===============

На этой странице, помимо ``PowerOfAttorney``, описаны следующие структуры и перечисления:

.. contents:: :local:


Структура ``PowerOfAttorney`` хранит информацию о машиночитаемой доверенности (МЧД).

.. code-block:: protobuf

    message PowerOfAttorney {
        required PowerOfAttorneyFullId FullId = 1;
        required PowerOfAttorneyIssuer Issuer = 2;
        required PowerOfAttorneyConfidant Confidant = 3;
        required Timestamp StartAt = 4;
        required Timestamp ExpireAt = 5;
        optional string System = 6;
        optional string IdFile = 7;
        repeated PowerOfAttorney DelegationChain = 8;
        required PowerOfAttorneyPermissionsInfo PermissionsInfo = 9;
        optional PowerOfAttorneyDelegationInfo DelegationInfo = 10;
    }

- ``FullId`` — идентификатор МЧД, представленный структурой :doc:`PowerOfAttorneyFullId`.
- ``Issuer`` — данные о доверителе, представленные структурой :ref:`PowerOfAttorneyIssuer`.
- ``Confidant`` — данные о представителе, представленные структурой :ref:`PowerOfAttorneyConfidant`.
- ``StartAt`` — дата начала действия МЧД, представленная структурой :doc:`Timestamp`.
- ``ExpireAt`` — срок действия МЧД, представленный структурой :doc:`Timestamp`.
- ``System`` — информация о системе хранения доверенности.
- ``IdFile`` — имя XML-файла МЧД без расширения.
- ``DelegationChain`` — список предыдущих МЧД для доверенности, выпущенной в порядке передоверия. Каждая МЧД представлена структурой ``PowerOfAttorney``. Список хранится в порядке от корневой МЧД (элемент с индексом ``0``) к дочерней, сама конечная МЧД в список не включена.  Заполняется только в случаях:

	- если при отправке документов в поле ``Contents`` структуры :doc:`PowerOfAttorneyToPost` была указана цепочка файлов МЧД;
	- если по идентификатору ``FullId`` удалось получить цепочку доверенностей из сервиса ФНС.

- ``PermissionsInfo`` — информация о полномочиях из МЧД, представленная структурой :doc:`PowerOfAttorneyPermissionsInfo`.
- ``DelegationInfo`` — информация о предыдущих МЧД для доверенности, выпущенной в порядке передоверия. Представлена структурой :ref:`PowerOfAttorneyDelegationInfo`. Заполняется только в случае, если МЧД выпущена в порядке передоверия. Для цепочки передоверия из двух МЧД совпадают номера корневой доверенности и доверенности, на основании которой осуществляется передоверие.


.. _PowerOfAttorneyIssuer:

PowerOfAttorneyIssuer
---------------------

Структура ``PowerOfAttorneyIssuer`` хранит данные о доверителе.

.. code-block:: protobuf

    message PowerOfAttorneyIssuer {
        optional PowerOfAttorneyIssuerType Type = 1 [default = UnknownIssuerType];
        optional PowerOfAttorneyIssuerLegalEntity LegalEntity = 2;
        optional PowerOfAttorneyIssuerForeignEntity ForeignEntity = 3;
        optional PowerOfAttorneyIssuerIndividualEntity IndividualEntity = 4;
        optional PowerOfAttorneyIssuerPhysicalEntity PhysicalEntity = 5;
    }

- ``Type`` — тип доверителя, принимает значение из перечисления :ref:`PowerOfAttorneyIssuerType`.
- ``LegalEntity`` — данные о юридическом лице, представленные структурой :ref:`PowerOfAttorneyIssuerLegalEntity`. Заполняется только в случае, если тип доверителя имеет значение ``Type = LegalEntity``.
- ``ForeignEntity`` — данные об иностранной организации, представленные структурой :ref:`PowerOfAttorneyIssuerForeignEntity`. Заполняется только в случае, если тип доверителя имеет значение ``Type = ForeignEntity``.
- ``IndividualEntity`` — данные об индивидуальном предпринимателе, представленные структурой :ref:`PowerOfAttorneyIssuerIndividualEntity`. Заполняется в случае, если тип доверителя имеет значение ``Type = IndividualEntity``.
- ``PhysicalEntity`` — данные о физическом лице, представленные структурой :ref:`PowerOfAttorneyIssuerPhysicalEntity`. Заполняется в случае, если тип доверителя имеет значение ``Type = PhysicalEntity``.


.. _PowerOfAttorneyIssuerType:

PowerOfAttorneyIssuerType
-------------------------

Перечисление ``PowerOfAttorneyIssuerType`` представляет собой тип доверителя.

.. code-block:: protobuf

    enum PowerOfAttorneyIssuerType {
        UnknownIssuerType = 0;
        LegalEntity = 1;
        ForeignEntity = 2;
        IndividualEntity = 3;
        PhysicalEntity = 4;
    }

- ``LegalEntity`` — юридическое лицо;
- ``ForeignEntity`` — иностранная организация;
- ``IndividualEntity`` — индивидуальный предприниматель;
- ``PhysicalEntity`` — физическое лицо.


.. _PowerOfAttorneyIssuerLegalEntity:

PowerOfAttorneyIssuerLegalEntity
--------------------------------

Структура ``PowerOfAttorneyIssuerLegalEntity`` хранит данные о юридическом лице, являющимся доверителем.

.. code-block:: protobuf

    message PowerOfAttorneyIssuerLegalEntity {
        required string Inn = 1;
        required string Kpp = 2;
        required string OrganizationName = 3;
    }

- ``Inn`` — ИНН доверителя.
- ``Kpp`` — КПП доверителя.
- ``OrganizationName`` — наименование организации.


.. _PowerOfAttorneyIssuerForeignEntity:

PowerOfAttorneyIssuerForeignEntity
----------------------------------

Структура ``PowerOfAttorneyIssuerForeignEntity`` хранит данные об иностранной организации, являющейся доверителем.

.. code-block:: protobuf

    message PowerOfAttorneyIssuerForeignEntity {
        optional string Inn = 1;
        optional string Kpp = 2;
        required string OrganizationName = 3;
    }

- ``Inn`` — ИНН доверителя.
- ``Kpp`` — КПП доверителя.
- ``OrganizationName`` — наименование организации.


.. _PowerOfAttorneyIssuerIndividualEntity:

PowerOfAttorneyIssuerIndividualEntity
-------------------------------------

Структура ``PowerOfAttorneyIssuerIndividualEntity`` хранит данные об индивидуальном предпринимателе, являющимся доверителем.

.. code-block:: protobuf

    message PowerOfAttorneyIssuerIndividualEntity {
        required string Inn = 1;
        required string OrganizationName = 3;
    }

- ``Inn`` — ИНН доверителя.
- ``OrganizationName`` — наименование индивидуального предпринимателя.


.. _PowerOfAttorneyIssuerPhysicalEntity:

PowerOfAttorneyIssuerPhysicalEntity
-----------------------------------

Структура ``PowerOfAttorneyIssuerPhysicalEntity`` хранит данные о физическом лице, являющимся доверителем.

.. code-block:: protobuf

    message PowerOfAttorneyIssuerPhysicalEntity {
        required string Inn = 1;
        optional FullName PersonName = 2;
    }

- ``Inn`` — ИНН доверителя.
- ``PersonName`` — ФИО доверителя, представленные структурой :doc:`FullName`.


.. _PowerOfAttorneyConfidant:

PowerOfAttorneyConfidant
------------------------

Структура ``PowerOfAttorneyConfidant`` хранит данные о представителе.

.. code-block:: protobuf

    message PowerOfAttorneyConfidant {
        required FullName PersonName = 1;
        required string Inn = 2;
        optional PowerOfAttorneyConfidantOrganization Organization = 3;
    }

- ``PersonName`` — ФИО представителя, представленные структурой :doc:`FullName`.
- ``Inn`` — ИНН представителя: физического или юридического лица. В случае юридического лица используется ИНН уполномоченного представителя этой организации, который может действовать без доверенности.
- ``Organization`` — данные об организации, представленные структурой :ref:`PowerOfAttorneyConfidantOrganization`. Заполняется только в случае, если представителем является организация.


.. _PowerOfAttorneyConfidantOrganization:

PowerOfAttorneyConfidantOrganization
------------------------------------

Структура ``PowerOfAttorneyConfidantOrganization`` хранит данные об организации-представителе.

.. code-block:: protobuf

    message PowerOfAttorneyConfidantOrganization {
        required string Inn = 1;
        optional string Kpp = 2;
        required string Name = 3;
    }

- ``Inn`` — ИНН представителя.
- ``Kpp`` — КПП представителя.
- ``Name`` — наименование организации.


.. _PowerOfAttorneyDelegationInfo:

PowerOfAttorneyDelegationInfo
-----------------------------

Структура ``PowerOfAttorneyDelegationInfo`` хранит данные о предыдущих МЧД.

.. code-block:: protobuf

    message PowerOfAttorneyDelegationInfo {
        required string RootRegistrationNumber = 1;
        optional string ParentRegistrationNumber = 2;
    }

- ``RootRegistrationNumber`` — регистрационный номер корневой (первоначальной) доверенности.
- ``ParentRegistrationNumber`` — регистрационный номер доверенности, на основании которой осуществляется передоверие.


----

.. rubric:: См. также

*Структура используется:*
	- в структуре :doc:`EmployeePowerOfAttorney`
	- в структуре :doc:`PowerOfAttorneyRegisterResult`
	- в теле ответа метода :doc:`../http/GetPowerOfAttorneyInfo`

*Инструкции:*
	- :doc:`../instructions/powerofattorney`