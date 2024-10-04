FullName
========

Структура ``FullName`` содержит информацию о полном имени.

.. code-block:: protobuf

    message FullName {
        required string LastName = 1;
        required string FirstName = 2;
        optional string MiddleName = 3;
    }

- ``LastName`` — фамилия.
- ``FirstName`` — имя.
- ``MiddleName`` — отчество.


----

.. rubric:: См. также

*Структура используется:*
	- в структуре :doc:`EmployeeToCreateByLogin <EmployeeToCreate>`
	- в структуре :doc:`PowerOfAttorneyConfidant <PowerOfAttorney>`
	- в структуре :doc:`PowerOfAttorneyIssuerPhysicalEntity <PowerOfAttorney>`
	- в структуре :doc:`UserV2`
	- в устаревшей структуре :doc:`UserFullNamePatch <obsolete/UserToUpdate>`