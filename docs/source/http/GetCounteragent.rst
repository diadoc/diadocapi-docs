GetCounteragent
===============

Метод ``GetCounteragent`` возвращает информацию о :doc:`контрагенте <../entities/counteragent>`.

.. http:get:: /V3/GetCounteragent

	:queryparam myBoxId: идентификатор :doc:`ящика <../../entities/box>` организации, для которой осуществляется поиск контрагента.
	:queryparam counteragentBoxId: идентификатор :doc:`ящика <../../entities/box>` организации контрагента.

	:requestheader Authorization: данные, необходимые для :doc:`авторизации <../Authorization>`.

	:statuscode 200: операция успешно завершена.
	:statuscode 400: данные в запросе имеют неверный формат или отсутствуют обязательные параметры.
	:statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization`` или в этом заголовке содержатся некорректные авторизационные данные.
	:statuscode 402: у организации с указанным идентификатором ``myBoxId`` закончилась подписка на API.
	:statuscode 403: доступ к списку контрагентов организации ``myBoxId`` с предоставленным авторизационным токеном запрещен.
	:statuscode 404: партнерские отношения между организациями ``myBoxId`` и ``counteragentBoxId`` не установлены.
	:statuscode 405: используется неподходящий HTTP-метод.
	:statuscode 500: при обработке запроса возникла непредвиденная ошибка.

	:response Body: Тело ответа содержит информацию о контрагенте с идентификатором ``counteragentBoxId`` для организации ``myBoxId``, представленную структурой :doc:`../proto/Counteragent`. Вложенная в нее структура :doc:`Counteragent.Organization.Departments <../proto/Organization>` содержит только видимые подразделения и их родительские подразделения.

.. include:: ../include/accessMethod_required_box.txt


----

.. rubric:: См. также

.. include:: ../include/seealso_counteragents.txt

*Устаревшие версии метода:*
	- :doc:`obsolete/GetCounteragent`
	- :doc:`obsolete/GetCounteragent_v2`