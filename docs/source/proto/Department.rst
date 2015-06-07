Department
==========

.. code-block:: protobuf

    message Department
    {
        required string DepartmentId = 1;
        required string ParentDepartmentId = 2;
        required string Name = 3;
        optional string Abbreviation = 4;
        optional string Kpp = 5;
        optional Address Address = 6;
    }
        

Структура данных *Department* содержит информацию о подразделении организации.

-  *DepartmentId* - уникальный идентификатор подразделения.

-  *ParentDepartmentId* - идентификатор родительского подразделения.

    Если родительское подразделение - головное, то идентификатор имеет вид 00000000-0000-0000-0000-000000000000

-  *Name* - полное наименование подразделения.

-  *Abbreviation* - сокращенное наименование подразделения (может отсутствовать).

-  *Kpp* - КПП подразделения (может отсутствовать).

-  :doc:`Address` - адрес подразделения (может отсутствовать).