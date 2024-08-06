DeleteCounteragentGroup
=======================

Метод ``DeleteCounteragentGroup`` удаляет группу контрагентов.

.. http:post:: /DeleteCounteragentGroup

	:queryparam boxId: идентификатор :doc:`ящика <../../entities/box>` организации.
	:queryparam counteragentGroupId: идентификатор группы контрагентов.

	:requestheader Authorization: данные, необходимые для :doc:`авторизации <../Authorization>`.

	:statuscode 200: операция успешно завершена.
	:statuscode 400: данные в запросе имеют неверный формат или отсутствуют обязательные параметры.
	:statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization`` или в этом заголовке содержатся некорректные авторизационные данные.
	:statuscode 402: у организации с указанным идентификатором ``boxId`` закончилась подписка на API.
	:statuscode 403: доступ к ящику с предоставленным авторизационным токеном запрещен или запрос сделан не от имени администратора.
	:statuscode 404: не найдена группа контрагентов с идентификатором ``CounteragentGroupId``.
	:statuscode 405: используется неподходящий HTTP-метод.
	:statuscode 409: нельзя удалить группу по умолчанию.
	:statuscode 500: при обработке запроса возникла непредвиденная ошибка.

.. include:: ../include/accessMethod_required_admin_manageCounteragents.txt

После удаления группы все контрагенты, находящиеся в ней, будут перемещены в группу «По умолчанию».


Примеры использования
---------------------

**Пример HTTP-запроса:**

.. literalinclude:: ../include/deleteCounteragentGroup_query.txt



----

.. rubric:: См. также

.. include:: ../include/seealso_method_counteragentgroup.txt
