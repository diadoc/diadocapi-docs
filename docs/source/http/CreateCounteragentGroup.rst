CreateCounteragentGroup
=======================

Метод ``CreateCounteragentGroup`` создает группу контрагентов.

.. http:post:: /CreateCounteragentGroup

	:queryparam boxId: идентификатор ящика организации.

	:requestheader Authorization: данные, необходимые для :doc:`авторизации <../Authorization>`.

	:request Body: Тело запроса должно содержать структуру ``CounteragentGroupToCreate``:

		.. code-block:: protobuf

		    message CounteragentGroupToCreate {
		        required string Name = 1;
 		        optional DepartmentsInGroup Departments = 2;
		    }

		    message DepartmentsInGroup {
		        repeated string DepartmentId = 1;
		    }

		..

		- ``Name`` — имя группы. Должно быть уникально в рамках одного ящика. Длина не должна превышать 500 символов.
		- ``Departments`` — подразделения, в которые контрагенты группы могут отправлять документы. Представлены структурой ``DepartmentsInGroup`` с полями:

			- ``DepartmentId`` — список идентификаторов подразделений.

	:statuscode 200: операция успешно завершена.
	:statuscode 400: данные в запросе имеют неверный формат или отсутствуют обязательные параметры.
	:statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization`` или в этом заголовке содержатся некорректные авторизационные данные.
	:statuscode 402: у организации с указанным идентификатором ``boxId`` закончилась подписка на API.
	:statuscode 403: доступ к ящику с предоставленным авторизационным токеном запрещен или запрос сделан не от имени администратора.
	:statuscode 404: не найдены подразделения с идентификатором ``DepartmentId``.
	:statuscode 405: используется неподходящий HTTP-метод.
	:statuscode 409: группа контрагентов с наименованием ``name`` уже существует.
	:statuscode 500: при обработке запроса возникла непредвиденная ошибка.

	:response Body: Тело ответа содержит структуру :doc:`../proto/CounteragentGroup`.

Создать группу контрагентов может только администратор ящика.

----

.. rubric:: Смотри также

*Другие методы для работы с группой контрагентов:*
	- :doc:`UpdateCounteragentGroup`,
	- :doc:`DeleteCounteragentGroup`,
	- :doc:`AddCounteragentsInGroup`,
	- :doc:`GetCounteragentGroups`,
	- :doc:`GetCounteragentsInGroup`.