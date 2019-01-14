DepartmentToCreate
==================

.. code-block:: protobuf

    message DepartmentToCreate
    {
        optional string ParentDepartmentId = 1;
        required string Name = 2;
        required string Abbreviation = 3;
        optional string Kpp = 4;
        optional Address Address = 5;
        required Routing Routing = 6;
    }

Структура *DepartmentToCreate* содержит информацию для создания подразделения.

- *ParentDepartmentId* - идентификатор родительского подразделения. Если не указано, будет создано подразделение c "ParentDepartmentId": "00000000-0000-0000-0000-000000000000".
- *Name* - название подразделения.
- *Abbreviation* - короткое название подразделения.
- *Kpp* - кпп подразделения.
- :doc:`Address <../Address>` - адрес подразделения.
- :doc:`Routing <Routing>` - тип доступной маршрутизации.