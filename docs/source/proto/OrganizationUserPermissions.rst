OrganizationUserPermissions
===========================

.. code-block:: protobuf

    enum DocumentAccessLevel {
        DepartmentOnly = 0;
        DepartmentAndSubdepartments = 1;
        AllDocuments = 2;
        UnknownDocumentAccessLevel = 3;
        SelectedDepartments = 3;
    }

    message OrganizationUserPermissions {
        required string UserDepartmentId = 1;
        required bool IsAdministrator = 2;
        optional DocumentAccessLevel DocumentAccessLevel = 3 [default = UnknownDocumentAccessLevel];
        required bool CanSignDocuments = 4;
        required bool CanAddResolutions = 7;
        required bool CanRequestResolutions = 8;
        repeated string SelectedDepartmentIds = 9;
    }
        

Структура данных *OrganizationUserPermissions* содержит информацию о правах пользователя в организации.

-  *UserDepartmentId* - идентификатор подразделения организации, в котором состоит пользователь.

	В случае головного подразделения содержит значение 00000000-0000-0000-0000-000000000000.

-  *IsAdministrator* - может ли пользователь редактировать структуру и реквизиты организации, добавлять и редактировать других пользователей.

-  *DocumentAccessLevel*:

   -  *UnknownDocumentAccessLevel* - неизвестный набор прав пользователя; 
   
   может выдаваться лишь в случае, когда клиент использует устаревшую версию SDK и не может интерпретировать переданный сервером уровень прав доступа.

   -  *DepartmentOnly* - пользователю доступны только документы из подразделения, в котором он состоит.

   -  *DepartmentAndSubdepartments* - пользователю доступны документы из подразделения, в котором он состоит и всех дочерних подразделений.

   -  *AllDocuments* - пользователю доступны все документы организации.

   -  *SelectedDepartments* - пользователю доступны документы из нескольких подразделений.

-  *CanSignDocuments* - может ли пользователь подписывать документы.

-  *CanAddResolutions* - может ли пользователь согласовывать документы.

-  *CanRequestResolutions* - может ли пользователь отправлять запросы на согласование и подпись документов.

-  *SelectedDepartmentIds* - список подразделений, к которым имеет доступ пользователь (заполняется только в случае *DocumentAccessLevel = SelectedDepartments*).
