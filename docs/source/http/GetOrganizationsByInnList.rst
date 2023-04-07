GetOrganizationsByInnList
=========================

Метод ``GetOrganizationsByInnList`` позволяет получить статус контрагентов в Диадоке по списку ИНН.

.. http:post:: /GetOrganizationsByInnList

	:queryparam myOrgId: идентификатор организации, для которой нужно получить статус контрагентов.

	:requestheader Authorization: данные, необходимые для :doc:`авторизации <../Authorization>`.

	:request Body: Тело запроса должно содержать структуру ``GetOrganizationsByInnListRequest``:

		.. code-block:: protobuf

		    message GetOrganizationsByInnListRequest {
		        repeated string InnList = 1;
		    }

		..

		- ``InnList`` — список ИНН организаций.

	:statuscode 200: операция успешно завершена.
	:statuscode 400: данные в запросе имеют неверный формат или отсутствуют обязательные параметры.
	:statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization`` или в этом заголовке содержатся некорректные авторизационные данные.
	:statuscode 402: у организации с указанным идентификатором ``boxId`` закончилась подписка на API.
	:statuscode 405: используется неподходящий HTTP-метод.
	:statuscode 500: при обработке запроса возникла непредвиденная ошибка.

	:response Body: Тело ответа содержит структуру :doc:`../proto/GetOrganizationsByInnListResponse`.

Если при вызове метода не передать параметр строки запроса ``myOrgId``, то в теле ответа вернется структура :doc:`../proto/GetOrganizationsByInnListResponse`, где для вложенной структуры ``OrganizationWithCounteragentStatus`` значение поля ``CounteragentStatus`` для всех организаций будет равно ``NotInCounteragentList``.

