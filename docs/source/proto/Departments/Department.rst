Department
==========

.. code-block:: protobuf

    message Department
    {
        required string Id = 1; 
        optional string ParentDepartmentId = 2;
        required string Name = 3;
        required string Abbreviation = 4;
        optional string Kpp = 5;
        optional Address Address = 6;
        required Routing Routing = 7;
        required Timestamp CreationTimestamp = 8;
    }

Структура *Department* содержит информацию о подразделени.

- *Id* - идентификатор подразделения. В случае головного подразделения содержит значение 00000000-0000-0000-0000-000000000000.
- *ParentDepartmentId* - идентификатор родительского подразделения.
- *Name* - название подразделения.
- *Abbreviation* - короткое название подразделения.
- *Kpp* - кпп подразделения.
- :doc:`Address <../Address>` - адрес подразделения.
- :doc:`Routing <Routing>` - тип доступной маршрутизации.
- :doc:`CreationTimestamp <../Timestamp>` - дата и время создания подразделения. Для головного подразделения значение этого поля null.