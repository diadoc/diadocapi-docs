BreakWithCounteragent
=====================

Метод ``BreakWithCounteragent`` разрывает отношения между :doc:`контрагентами <../entities/counteragent>`, а также для отзывает или отклоняет приглашения к партнерству без вложения.

Чтобы отозвать приглашение с вложением, сгенерируйте запрос методом :doc:`GenerateRevocationRequestXml` и отправьте его методом :doc:`PostMessagePatch`.

.. http:post:: /V2/BreakWithCounteragent

	:queryparam myBoxId: идентификатор :doc:`ящика <../../entities/box>` организации, от имени которой производится разрыв отношения партнерства.
	:queryparam counteragentBoxId: идентификатор :doc:`ящика <../../entities/box>` организации контрагента.
	:queryparam comment: текст комментария к операции. Необязательный параметр, длина не более 5000 символов.

	:requestheader Authorization: данные, необходимые для :doc:`авторизации <../Authorization>`.

	:statuscode 200: операция успешно завершена.
	:statuscode 400: данные в запросе имеют неверный формат или отсутствуют обязательные параметры.
	:statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization`` или в этом заголовке содержатся некорректные авторизационные данные.
	:statuscode 402: у организации с указанным идентификатором ``myOrgId`` закончилась подписка на API.
	:statuscode 403: доступ к списку контрагентов организации ``myOrgId`` с предоставленным авторизационным токеном запрещен или у пользователя нет права работать со списками контрагентов (см. :doc:`OrganizationUserPermissions.CanManageCounteragents <../proto/OrganizationUserPermissions>`).
	:statuscode 405: используется неподходящий HTTP-метод.
	:statuscode 409: метод используется для отзыва приглашения с вложением.
	:statuscode 500: при обработке запроса возникла непредвиденная ошибка.

.. include:: ../include/accessMethod_required_manageCounteragents.txt

Метод работает по следующим правилам:

	- Если между организациями ``myOrgId`` и ``counteragentOrgId`` есть действующее отношение партнерства (контрагент ``counteragentOrgId`` находится в статусе ``IsMyCounteragent``), оно разрывается. Контрагент ``counteragentOrgId`` переходит в статус ``IsRejectedByMe``.
	- Если в индексе отношений есть входящий запрос на установление отношения партнерства от организации ``counteragentOrgId`` к организации ``myOrgId`` (контрагент ``counteragentOrgId`` находится в статусе ``InvitesMe``), то этот запрос отклоняется. Контрагент ``counteragentOrgId`` переходит в статус ``IsRejectedByMe``.
	- Если в индексе отношений есть исходящий запрос от организации ``myOrgId`` к организации ``counteragentOrgId`` (контрагент ``counteragentOrgId`` находится в статусе ``IsInvitedByMe``), то выполняется отзыв этого запроса. Статус контрагента ``counteragentOrgId`` меняется на статус, который был до отправки запроса.
	- Если партнерских отношений между организациями ``myOrgId`` и ``counteragentOrgId`` нет или они уже разорваны, то после вызова метода ничего не произойдет.


----

.. rubric:: См. также

.. include:: ../include/seealso_counteragents.txt

*Устаревшие версии метода:*
	- :doc:`obsolete/BreakWithCounteragent`