GetCounteragent
===============

Метод ``GetCounteragent`` возвращает информацию о :doc:`контрагенте <../entities/counteragent>`.

Версии метода:
	- :ref:`GetCounteragent_v2` — возвращает для контрагента только видимые подразделения и их родительские подразделения.
	- :ref:`GetCounteragent_v1` — возвращает все подразделения контрагента.

.. _GetCounteragent_v2:

v2
--

.. http:get:: /V2/GetCounteragent

	:queryparam myOrgId: идентификатор организации, для которой осуществляется поиск контрагента.
	:queryparam counteragentOrgId: идентификатор организации-контрагента.
	
	:requestheader Authorization: данные, необходимые для :doc:`авторизации <../Authorization>`.
	
	:statuscode 200: операция успешно завершена.
	:statuscode 400: данные в запросе имеют неверный формат или отсутствуют обязательные параметры.
	:statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization`` или в этом заголовке содержатся некорректные авторизационные данные.
	:statuscode 402: у организации с указанным идентификатором ``myOrgId`` закончилась подписка на API.
	:statuscode 403: доступ к списку контрагентов организации ``myOrgId`` с предоставленным авторизационным токеном запрещен.
	:statuscode 404: партнерские отношения между организациями ``myOrgId`` и ``counteragentOrgId`` не установлены.
	:statuscode 405: используется неподходящий HTTP-метод.
	:statuscode 500: при обработке запроса возникла непредвиденная ошибка.

	:response Body: Тело ответа содержит информацию о контрагенте с идентификатором ``counteragentOrgId`` для организации ``myOrgId``, представленную структурой :doc:`../proto/Counteragent`. Вложенная в нее структура :doc:`Counteragent.Organization.Departments <../proto/Organization>` содержит только видимые подразделения и их родительские подразделения.

Пользователь имеет право запрашивать и производить действия со списком контрагентов организации ``myOrgId``, если у него есть доступ к ящику этой организации.


.. _GetCounteragent_v1:

v1
--

.. http:get:: /GetCounteragent

	:queryparam myOrgId: идентификатор организации, для которой осуществляется поиск контрагента.
	:queryparam counteragentOrgId: идентификатор организации-контрагента.
	
	:requestheader Authorization: данные, необходимые для :doc:`авторизации <../Authorization>`.
	
	:statuscode 200: операция успешно завершена.
	:statuscode 400: данные в запросе имеют неверный формат или отсутствуют обязательные параметры.
	:statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization`` или в этом заголовке содержатся некорректные авторизационные данные.
	:statuscode 402: у организации с указанным идентификатором ``myOrgId`` закончилась подписка на API.
	:statuscode 403: доступ к списку контрагентов организации ``myOrgId`` с предоставленным авторизационным токеном запрещен.
	:statuscode 404: партнерские отношения между организациями ``myOrgId`` и ``counteragentOrgId`` не установлены.
	:statuscode 405: используется неподходящий HTTP-метод.
	:statuscode 500: при обработке запроса возникла непредвиденная ошибка.

	:response Body: Тело ответа содержит информацию о контрагенте с идентификатором ``counteragentOrgId`` для организации ``myOrgId``, представленную структурой :doc:`../proto/Counteragent`.

Пользователь имеет право запрашивать и производить действия со списком контрагентов организации ``myOrgId``, если у него есть доступ к ящику этой организации.