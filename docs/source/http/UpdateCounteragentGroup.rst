UpdateCounteragentGroup
=======================

Метод ``UpdateCounteragentGroup`` позволяет редактировать группу контрагентов.

.. http:post:: /UpdateCounteragentGroup

	:queryparam boxId: идентификатор :doc:`ящика <../../entities/box>` организации.
	:queryparam counteragentGroupId: идентификатор группы контрагентов.

	:requestheader Authorization: данные, необходимые для :doc:`авторизации <../Authorization>`.

	:request Body: Тело запроса должно содержать структуру ``CounteragentGroupToUpdate``:

		.. code-block:: protobuf

		    message  CounteragentGroupToUpdate {
		        optional string Name = 1;
		        optional CounteragentGroupDepartmentPatch GroupDepartments = 2;
		    }

		    message CounteragentGroupDepartmentPatch {
		        required bool AnyDepartment = 1;
		        optional DepartmentsInGroup Departments = 2;
		    }

		..

		- ``Name`` — название группы контрагентов.
		- ``GroupDepartments`` — подразделения, в которые контрагенты группы могут отправлять документы. Представлены структурой ``CounteragentGroupDepartmentPatch`` с полями:

			- ``AnyDepartment`` — флаг, указывающий, что документы можно отправлять в любое подразделение.
			- ``Departments`` — список подразделений, в которые контрагенты группы могут отправлять документы. Представлен структурой :doc:`../proto/DepartmentsInGroup`. Нельзя указывать одновременно с ``AnyDepartment = true``. В списке может быть не больше 419 подразделений.

	:statuscode 200: операция успешно завершена.
	:statuscode 400: данные в запросе имеют неверный формат или отсутствуют обязательные параметры, или невозможно изменить наименование группы по умолчанию.
	:statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization`` или в этом заголовке содержатся некорректные авторизационные данные.
	:statuscode 402: у организации с указанным идентификатором ``boxId`` закончилась подписка на API.
	:statuscode 403: доступ к ящику с предоставленным авторизационным токеном запрещен или запрос сделан не от имени администратора.
	:statuscode 404: не найдена группа контрагентов с идентификатором ``CounteragentGroupId`` или не найдены подразделения с идентификатором ``DepartmentId``.
	:statuscode 405: используется неподходящий HTTP-метод.
	:statuscode 409: группа контрагентов с наименованием ``Name`` уже существует.
	:statuscode 500: при обработке запроса возникла непредвиденная ошибка.

	:response Body: Тело ответа содержит структуру :doc:`../proto/CounteragentGroup`.

Изменить группу контрагентов может только администратор ящика с разрешением ``CanManageCounteragents``, позволяющим видеть списки контрагентов и работать с ними.

Изменить список подразделений, в которые группа может отправлять документы, можно одним из следующих способов:

	- Чтобы добавить или удалить подразделения, передайте структуру ``CounteragentGroupDepartmentPatch`` с флагом ``AnyDepartment = false`` и обновленным списком подразделений.
	- Чтобы изменить список подразделений на «любое подразделение», передайте структуру ``CounteragentGroupDepartmentPatch`` только с флагом ``AnyDepartment = true``.
	- Чтобы указать список конкретных подразделений для группы с разрешением отправлять документы в любое подразделение, передайте структуру ``CounteragentGroupDepartmentPatch`` с флагом ``AnyDepartment = false`` и списком подразделений.

----

.. rubric:: См. также

.. include:: ../reused_text/counteragentgroup_seealso.txt