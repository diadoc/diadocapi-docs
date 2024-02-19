GetCounteragentsInGroup
=======================

Метод ``GetCounteragentsInGroup`` предназначен для просмотра списка контрагентов в группе.

.. http:get:: /GetCounteragentsInGroup

	:queryparam boxId: идентификатор ящика организации.
	:queryparam CounteragentGroupId: идентификатор группы контрагентов
	:queryparam offset: номер страницы, которую нужно получить. Необязательный параметр. По умолчанию равен 1.
	:queryparam limit:  количество групп контрагентов на одной странице. Может принимать значения от 1 до 100. Необязательный параметр. По умолчанию равен 100.

	:requestheader Authorization: данные, необходимые для :doc:`авторизации <../Authorization>`.

	:statuscode 200: операция успешно завершена.
	:statuscode 400: данные в запросе имеют неверный формат или отсутствуют обязательные параметры, или невозможно изменить наименование группы по умолчанию.
	:statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization`` или в этом заголовке содержатся некорректные авторизационные данные.
	:statuscode 402: у организации с указанным идентификатором ``boxId`` закончилась подписка на API.
	:statuscode 404: не найдена группа контрагентов с идентификатором ``CounteragentGroupId``.
	:statuscode 405: используется неподходящий HTTP-метод.
	:statuscode 500: при обработке запроса возникла непредвиденная ошибка.

	:response Body: Тело ответа содержит структуру ``CounteragentInGroupResponse``:

		.. code-block:: protobuf

		    message CounteragentInGroupResponse { 
		        repeated string CounteragentId = 1;
		        required int32 TotalCount = 2;
		    }

		- ``CounteragentId`` — идентификатор контрагента.
		- ``TotalCount`` — количество контрагентов в группе.

Метод вернет идентификатор контрагента ``CounteragentId``, если ``CounteragentStatus = IsMyCounteragent``. Узнать статус можно с помощью метода :doc:`GetOrganizationsByInnList`.