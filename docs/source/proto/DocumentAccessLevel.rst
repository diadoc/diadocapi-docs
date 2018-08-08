DocumentAccessLevel
===================

.. code-block:: protobuf

    enum DocumentAccessLevel {
        UnknownDocumentAccessLevel = -1;
        DepartmentOnly = 0;
        DepartmentAndSubdepartments = 1;
        AllDocuments = 2;
        SelectedDepartments = 3;
    }

Перечисление обозначает уровень доступа сотрудника к документам организации. Возможные значения:

- *UnknownDocumentAccessLevel* - неизвестный набор прав пользователя. Может выдаваться лишь в случае, когда клиент использует устаревшую версию SDK и не может интерпретировать переданный сервером уровень прав доступа.
- *DepartmentOnly* - пользователю доступны только документы из подразделения, в котором он состоит.
- *DepartmentAndSubdepartments* - пользователю доступны документы из подразделения, в котором он состоит и всех дочерних подразделений.
- *AllDocuments* - пользователю доступны все документы организации.
- *SelectedDepartments* - пользователю доступны документы из нескольких подразделений.
