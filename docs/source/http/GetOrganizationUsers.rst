GetOrganizationUsers
====================

Метод ``GetOrganizationUsers`` возвращает пользователей указанной организации.

.. http:get:: /V2/GetOrganizationUsers

	:queryparam boxId: идентификатор организации.

	:requestheader Authorization: данные, необходимые для :doc:`авторизации <../Authorization>`.

	:statuscode 200: операция успешно завершена.
	:statuscode 400: данные в запросе имеют неверный формат или отсутствуют обязательные параметры.
	:statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization`` или в этом заголовке содержатся некорректные авторизационные данные.
	:statuscode 402: у организации с указанным идентификатором ``boxId`` закончилась подписка на API.
	:statuscode 404: не найден ящик с указанным идентификатором.
	:statuscode 405: используется неподходящий HTTP-метод.
	:statuscode 500: при обработке запроса возникла непредвиденная ошибка.

	:response Body: Тело ответа содержит список всех пользователей организации, представленный структурой :doc:`../proto/OrganizationUsersList`.


----

.. rubric:: См. также

*Устаревшие версии метода:*
	- :doc:`obsolete/GetOrganizationUsers`