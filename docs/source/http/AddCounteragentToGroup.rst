AddCounteragentToGroup
=======================

Метод ``AddCounteragentToGroup`` добавляет контрагента в группу.

.. http:post:: /AddCounteragentToGroup

	:queryparam boxId: идентификатор :doc:`ящика <../../entities/box>` организации.
	:queryparam counteragentGroupId: идентификатор группы контрагентов.
	:queryparam counteragentBoxId: идентификатор ящика контрагента.

	:requestheader Authorization: данные, необходимые для :doc:`авторизации <../Authorization>`.

	:statuscode 200: операция успешно завершена.
	:statuscode 400: данные в запросе имеют неверный формат или отсутствуют обязательные параметры.
	:statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization`` или в этом заголовке содержатся некорректные авторизационные данные.
	:statuscode 402: у организации с указанным идентификатором ``boxId`` закончилась подписка на API.
	:statuscode 403: доступ к ящику с предоставленным авторизационным токеном запрещен или запрос сделан не от имени администратора.
	:statuscode 404: не найдена группа контрагентов с идентификатором ``CounteragentGroupId``.
	:statuscode 405: используется неподходящий HTTP-метод.
	:statuscode 409: с контрагентом не установлены партнерские отношения.
	:statuscode 500: при обработке запроса возникла непредвиденная ошибка.

.. include:: ../include/accessMethod_counteragentGroups.txt

Метод ``AddCounteragentToGroup`` добавляет в группу только контрагентов со статусом ``CounteragentStatus = IsMyCounteragent``, иначе возвращает ошибку ``409 (Conflict )``. Узнать статус контрагента можно с помощью метода :doc:`GetOrganizationsByInnList`.


Примеры использования
---------------------

**Пример HTTP-запроса:**

.. literalinclude:: ../include/addCounteragentToGroup_query.txt


----

.. rubric:: См. также

.. include:: ../include/seealso_counteragentgroup.txt