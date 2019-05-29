DeprtmentToUpdate
=================

.. code-block:: protobuf

    message DeprtmentToUpdate
    {
        optional ParentDepartmentPatch ParentDepartment = 1;
        optional DepartmentNamingPatch DepartmentNaming = 2
        optional DepartmentKppPatch Kpp = 3;
        optional DepartmentAddressPatch Address = 4;
        optional DepartmentRoutingPatch Routing = 5;
    }

Структура *DeprtmentToUpdate* содержит информацию для редактирования подразделения.

- :ref:`ParentDepartment <parent-department-patch>`- патч идентификатора родительского подразделения.
- :ref:`Name <department-naming-patch>` - патч названия подразделения.
- :ref:`Kpp <department-kpp-patch>` - патч кпп подразделения.
- :ref:`Address <department-address-patch>` - патч адреса подразделения.
- :ref:`Routing <department-routing-patch>` - патч типа доступной маршрутизации.

.. _parent-department-patch:

ParentDepartmentPatch
---------------------

.. code-block:: protobuf

    message ParentDepartmentPatch
    {
        required string ParentDepartmentId = 1;
    }

Структура *ParentDepartmentPatch* содержит информацию для обновления родительского подразделения.

- *ParentDepartmentId* - новое значение родительского подразделения.

.. _department-naming-patch:

DepartmentNamingPatch
---------------------

.. code-block:: protobuf

    message DepartmentNamingPatch
    {
        required string Name = 1;
        required string Abbreviation = 2;
    }

Структура *DepartmentNamingPatch* содержит информацию для обновления названия и краткого названия подразделения.

- *Name* - новое название подразделения.
- *Abbreviation* - новое короткое название подразделения.

.. _department-kpp-patch:

DepartmentKppPatch
------------------

.. code-block:: protobuf

    message DepartmentKppPatch
    {
        optional string  Kpp = 1;
    }

Структура *DepartmentKppPatch* содержит информацию для обновления кпп подразделения.

- *Kpp* - новое КПП подразделения.

.. _department-address-patch:

DepartmentAddressPatch
----------------------

.. code-block:: protobuf

    message DepartmentAddressPatch
    {
        optional Address Address = 1;
    }

Структура *DepartmentAddressPatch* содержит информацию для обновления адреса подразделения.

- :doc:`Address <../Address>` - новый адрес подразделения.

.. _department-routing-patch:

DepartmentRoutingPatch
----------------------

.. code-block:: protobuf

    message DepartmentRoutingPatch
    {
        required bool Kpp = 1;
        required bool Address = 2;
    }

Структура *DepartmentRoutingPatch* содержит информацию для обвноления типа маршрутизации подразделения.

- *Kpp* - доступна ли маршрутизация по КПП.
- *Address* - доступна ли маршрутизация по адресу.