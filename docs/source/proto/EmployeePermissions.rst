EmployeePermissions
===================

.. code-block:: protobuf

    message EmployeePermissions {
        required string UserDepartmentId = 1;
        required bool IsAdministrator = 2;
        required DocumentAccessLevel DocumentAccessLevel = 3 [default = UnknownDocumentAccessLevel];
        repeated string SelectedDepartmentIds = 4;
        repeated EmployeeAction Actions = 5;
    }

    message EmployeeAction {
        required string Name = 1;
        required bool IsAllowed = 2;
    }

Структура *EmployeePermissions* содержит информацию о правах сотрудника организации. Как часть структуры :doc:`Employee` возвращается методом :doc:`../http/GetEmployee`.

- *UserDepartmentId* - идентификатор подразделения организации, в котором состоит сотрудник. В случае головного подразделения содержит значение 00000000-0000-0000-0000-000000000000
- *IsAdministrator* - может ли сотрудник редактировать структуру и реквизиты организации, добавлять и редактировать других сотрудников
- :doc:`DocumentAccessLevel` - уровень доступа к документам
- *SelectedDepartmentIds* - список подразделений, к которым имеет доступ сотрудник (заполняется только в случае *DocumentAccessLevel = SelectedDepartments*).
- *Actions* - информация о том, какие действия имеет право выполнять сотрудник

Структура *EmployeeAction* содержит информацию о том, может ли сотрудник совершить конкретное действие.

- *Name* - строковой идентификатор действия
- *IsAllowed* - разрешено ли действие

.. csv-table:: Действия сотрудников
   :header: "Идентификатор", "Описание"
   :widths: 2, 10

   "CreateDocuments", "Создавать документы и работать с черновиками"
   "SignDocuments", "Подписывать документы"
   "AddResolutions", "Согласовывать документы"
   "RequestResolutions", "Передавать на подпись и согласование"
   "ManageCounteragents", "Видеть списки контрагентов и работать с ними"