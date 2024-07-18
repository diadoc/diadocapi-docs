Department
==========

Структура ``Department`` содержит информацию о подразделении организации.

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

- ``DepartmentId`` — идентификатор подразделения.
- ``ParentDepartmentId`` — идентификатор родительского подразделения. Если родительским подразделением является головное, идентификатор будет иметь значение ``00000000-0000-0000-0000-000000000000``.
- ``Name`` — полное наименование подразделения.
- ``Abbreviation`` — сокращенное наименование подразделения.
- ``Kpp`` — КПП подразделения.
- ``Address``— адрес подразделения, представленный структурой :doc:`Address`.

----

.. rubric:: См. также

*Структура используется:*
	- в структуре :doc:`Organization`
	- в теле ответа метода :doc:`../http/GetDepartment`