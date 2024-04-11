GetCounteragentGroup
====================

Метод ``GetCounteragentGroup`` возвращает информацию о группе контрагентов.

.. http:get:: /GetCounteragentGroup

	:queryparam boxId: идентификатор :doc:`ящика <../../entities/box>` организации.
	:queryparam counteragentGroupId: идентификатор группы контрагентов.

	:requestheader Authorization: данные, необходимые для :doc:`авторизации <../Authorization>`.

	:statuscode 200: операция успешно завершена.
	:statuscode 400: данные в запросе имеют неверный формат или отсутствуют обязательные параметры.
	:statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization`` или в этом заголовке содержатся некорректные авторизационные данные.
	:statuscode 402: у организации с указанным идентификатором ``boxId`` закончилась подписка на API.
	:statuscode 403: доступ к ящику с предоставленным авторизационным токеном запрещен или запрос сделан не от имени сотрудника организации с разрешением ``CanManageCounteragents``.
	:statuscode 404: не найдена группа контрагентов с идентификатором ``CounteragentGroupId``.
	:statuscode 405: используется неподходящий HTTP-метод.
	:statuscode 500: при обработке запроса возникла непредвиденная ошибка.

	:response Body: Тело ответа содержит структуру :doc:`../proto/CounteragentGroup`.

Получить информацию о группе контрагентов может только сотрудник организации с разрешением ``CanManageCounteragents``, позволяющим видеть списки контрагентов и работать с ними.

----

.. rubric:: См. также

*Другие методы для работы с группой контрагентов:*
	- :doc:`CreateCounteragentGroup` — создает группу контрагентов
	- :doc:`UpdateCounteragentGroup` — редактирует группу контрагентов
	- :doc:`DeleteCounteragentGroup` — удаляет группу контрагентов
	- :doc:`AddCounteragentToGroup` — добавляет контрагентов в группу
	- :doc:`GetCounteragentGroups` — возвращает список групп контрагентов
	- :doc:`GetCounteragentsFromGroup` — возвращает список контрагентов в группе