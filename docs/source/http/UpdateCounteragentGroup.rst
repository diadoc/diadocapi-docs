UpdateCounteragentGroup
=======================

Метод ``UpdateCounteragentGroup`` предназначен для редактирования группы контрагентов.

.. http:post:: /UpdateCounteragentGroup

	:queryparam boxId: идентификатор ящика организации.
	:queryparam CounteragentGroupId: идентификатор группы контрагентов.

	:requestheader Authorization: данные, необходимые для :doc:`авторизации <../Authorization>`.

	:request Body: Тело запроса должно содержать структуру ``CounteragentGroupToUpdate``:

		.. code-block:: protobuf

		    message  CounteragentGroupToUpdate {  
		        optional string Name = 1;
		        optional CounteragentGroupDepartmentPatch Departments = 2;
		    }

		    message CounteragentGroupDepartmentPatch {
		        required bool AnyDepartment = 1;
		        optional DepartmentsInGroup DepartmentId = 2;
		    }

		..

		- ``Name`` — наименование группы контрагентов.
		- ``Departments`` — подразделения, в которые контрагенты группы могут отправлять документы. Представлены структурой ``CounteragentGroupDepartmentPatch`` с полями:

			- ``AnyDepartment`` — флаг, указывающий, что документы можно отправлять в любое подразделение.
			- ``DepartmentId`` — список подразделений, в которые контрагенты группы могут отправлять документы. Нельзя указывать одновременно с ``AnyDepartment = true``. Представлен структурой :doc:`../proto/DepartmentsInGroup`.

	:statuscode 200: операция успешно завершена.
	:statuscode 400: данные в запросе имеют неверный формат или отсутствуют обязательные параметры, или невозможно изменить наименование группы по умолчанию.
	:statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization`` или в этом заголовке содержатся некорректные авторизационные данные.
	:statuscode 402: у организации с указанным идентификатором ``boxId`` закончилась подписка на API.
	:statuscode 403: доступ к ящику с предоставленным авторизационным токеном запрещен или запрос сделан не от имени администратора.
	:statuscode 404: не найдена группа контрагентов с идентификатором ``CounteragentGroupId`` или не найдены подразделения с идентификатором ``DepartmentId``.
	:statuscode 405: используется неподходящий HTTP-метод.
	:statuscode 409: группа контрагентов с наименованием ``name`` уже существует.
	:statuscode 500: при обработке запроса возникла непредвиденная ошибка.

	:response Body: Тело ответа содержит структуру :doc:`../proto/CounteragentGroup`.

Изменить группу контрагентов может только администратор ящика.

Изменить список подразделений, в которые группа может отправлять документы, можно одним из следующих способов:

	- Чтобы добавить или удалить подразделения, передайте структуру ``CounteragentGroupDepartmentPatch`` с флагом ``AnyDepartment = false`` и обновленным списком подразделений.
	- Чтобы изменить список подразделений на «любое подразделение», передайте структуру ``CounteragentGroupDepartmentPatch`` только с параметром ``AnyDepartment = true``.
	- Если группа может отправлять документы в любое подразделение, то для указания списка подразделений передайте структуру ``CounteragentGroupDepartmentPatch`` с флагом ``AnyDepartment = false`` и списком конкретных подразделений.

----

.. rubric:: Смотри также

*Другие методы для работы с группой контрагентов:*
	- :doc:`CreateCounteragentGroup` — создает группу контрагентов,
	- :doc:`DeleteCounteragentGroup` — удаляет группу контрагентов,
	- :doc:`AddCounteragentsInGroup` — добавляет контрагентов в группу,
	- :doc:`GetCounteragentGroups` — возвращает список групп контрагентов,
	- :doc:`GetCounteragentsInGroup` — возвращает список контрагентов в группе.
