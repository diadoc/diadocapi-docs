CreateCounteragentGroup
=======================

Метод ``CreateCounteragentGroup`` создает группу контрагентов.

.. http:post:: /CreateCounteragentGroup

	:queryparam boxId: идентификатор :doc:`ящика <../../entities/box>` организации.

	:requestheader Authorization: данные, необходимые для :doc:`авторизации <../Authorization>`.

	:request Body: Тело запроса должно содержать структуру ``CounteragentGroupToCreate``:

		.. code-block:: protobuf

		    message CounteragentGroupToCreate {
		        required string Name = 1;
 		        optional DepartmentsInGroup Departments = 2;
		    }

		..

		- ``Name`` — название группы контрагентов. Должно быть уникальным в рамках одного ящика. Длина не должна превышать 1024 символов.
		- ``Departments`` — список подразделений, в которые контрагенты группы могут отправлять документы. Представлен структурой :doc:`../proto/DepartmentsInGroup`. В списке может быть не больше 419 подразделений. Если не заполнено, контрагенты из группы смогут отправлять документы в любое подразделение.

	:statuscode 200: операция успешно завершена.
	:statuscode 400: данные в запросе имеют неверный формат или отсутствуют обязательные параметры.
	:statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization`` или в этом заголовке содержатся некорректные авторизационные данные.
	:statuscode 402: у организации с указанным идентификатором ``boxId`` закончилась подписка на API.
	:statuscode 403: доступ к ящику с предоставленным авторизационным токеном запрещен или запрос сделан не от имени администратора.
	:statuscode 404: не найдены подразделения с идентификатором ``DepartmentId`` или подразделение было удалено.
	:statuscode 405: используется неподходящий HTTP-метод.
	:statuscode 409: группа контрагентов с наименованием ``name`` уже существует.
	:statuscode 500: при обработке запроса возникла непредвиденная ошибка.

	:response Body: Тело ответа содержит структуру :doc:`../proto/CounteragentGroup`.

Создать группу контрагентов может только администратор ящика с разрешением ``CanManageCounteragents``, позволяющим видеть списки контрагентов и работать с ними.

----

.. rubric:: См. также

*Другие методы для работы с группой контрагентов:*
	- :doc:`AddCounteragentToGroup` — добавляет контрагентов в группу
	- :doc:`DeleteCounteragentGroup` — удаляет группу контрагентов
	- :doc:`GetCounteragentGroup` — возвращает информацию о группе контрагентов
	- :doc:`GetCounteragentGroups` — возвращает список групп контрагентов
	- :doc:`GetCounteragentsFromGroup` — возвращает список контрагентов в группе
	- :doc:`UpdateCounteragentGroup` — редактирует группу контрагентов