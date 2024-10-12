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

- :ref:`ParentDepartment <ParentDepartmentPatch>`- патч идентификатора родительского подразделения.
- :ref:`Name <DepartmentNamingPatch>` - патч названия подразделения.
- :ref:`Kpp <DepartmentKppPatch>` - патч кпп подразделения.
- :ref:`Address <DepartmentAddressPatch>` - патч адреса подразделения.
- :ref:`Routing <DepartmentRoutingPatch>` - патч типа доступной маршрутизации.


.. _ParentDepartmentPatch:

ParentDepartmentPatch
---------------------

.. code-block:: protobuf

    message ParentDepartmentPatch
    {
        required string ParentDepartmentId = 1;
    }

Структура *ParentDepartmentPatch* содержит информацию для обновления родительского подразделения.

- *ParentDepartmentId* - новое значение родительского подразделения.


.. _DepartmentNamingPatch:

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


.. _DepartmentKppPatch:

DepartmentKppPatch
------------------

.. code-block:: protobuf

    message DepartmentKppPatch
    {
        optional string  Kpp = 1;
    }

Структура *DepartmentKppPatch* содержит информацию для обновления кпп подразделения.

- *Kpp* - новое КПП подразделения.


.. _DepartmentAddressPatch:

DepartmentAddressPatch
----------------------

.. code-block:: protobuf

    message DepartmentAddressPatch
    {
        optional Address Address = 1;
    }

Структура *DepartmentAddressPatch* содержит информацию для обновления адреса подразделения.

- :doc:`Address <../Address>` - новый адрес подразделения.


.. _DepartmentRoutingPatch:

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