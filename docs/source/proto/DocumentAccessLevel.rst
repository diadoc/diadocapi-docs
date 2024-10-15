DocumentAccessLevel
===================

Перечисление ``DocumentAccessLevel`` представляет собой уровень доступа сотрудника к документам организации.

.. code-block:: protobuf

    enum DocumentAccessLevel {
        UnknownDocumentAccessLevel = -1;
        DepartmentOnly = 0;
        DepartmentAndSubdepartments = 1;
        AllDocuments = 2;
        SelectedDepartments = 3;
    }

- ``UnknownDocumentAccessLevel`` — неизвестный набор прав пользователя. Возвращается в случае, если клиент использует устаревшую версию SDK и не может интерпретировать переданный сервером уровень прав доступа.
- ``DepartmentOnly`` — пользователю доступны только документы из подразделения, в котором он состоит.
- ``DepartmentAndSubdepartments`` — пользователю доступны документы из подразделения, в котором он состоит, и из всех его дочерних подразделений.
- ``AllDocuments`` — пользователю доступны все документы организации.
- ``SelectedDepartments`` — пользователю доступны документы из нескольких подразделений.

----

.. rubric:: См. также

*Перечисление используется:*
	- в структуре :doc:`EmployeeDocumentAccessLevelPatch <EmployeeToUpdate>`
	- в структуре :doc:`EmployeePermissions`
	- в структуре :doc:`OrganizationUserPermissions`