DeleteDepartment
================

.. note::
	Вызов метода доступен только администраторам организации.

Метод ``DeleteDepartment`` удаляет подразделение оранизации.
	
.. http:post:: /admin/DeleteDepartment

	:queryparam boxId: идентификатор :doc:`ящика <../../entities/box>` организации.
	:queryparam departmentId: идентификатор подразделения организации.

	:requestheader Authorization: данные, необходимые для :doc:`авторизации <../../Authorization>`.

	:statuscode 200: операция успешно завершена.
	:statuscode 400: данные в запросе имеют неверный формат или отсутствуют обязательные параметры.
	:statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization`` или в этом заголовке содержатся некорректные авторизационные данные.
	:statuscode 402: у организации с указанным идентификатором ``boxId`` закончилась подписка на API.
	:statuscode 403: доступ к ящику с предоставленным авторизационным токеном запрещен или запрос сделан не от имени администратора.
	:statuscode 404: в указанном ящике нет подразделения с указанным идентификатором.
	:statuscode 405: используется неподходящий HTTP-метод.
	:statuscode 409: см. примечания ниже.
	:statuscode 500: при обработке запроса возникла непредвиденная ошибка.

Примечания:
	-  Нельзя удалить головное подразделение с идентификатором ``00000000-0000-0000-0000-000000000000``.
	-  Нельзя удалить подразделение, содержащее дочерние подразделения.
	-  Нельзя удалить подразделение, в котором есть документы и сотрудники.