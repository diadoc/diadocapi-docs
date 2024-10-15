GetCounteragentsFromGroup
=========================

Метод ``GetCounteragentsFromGroup`` возращает список контрагентов, состоящих в указанной в группе.

.. http:get:: /GetCounteragentsFromGroup

	:queryparam boxId: идентификатор :doc:`ящика <../../entities/box>` организации.
	:queryparam counteragentGroupId: идентификатор группы контрагентов
	:queryparam afterIndexKey: уникальный ключ, позволяющий итерироваться по списку контрагентов. Необязательный параметр.
	:queryparam count: максимальное количество контрагентов в ответе. Может принимать значения от 1 до 100. Необязательный параметр. По умолчанию равен 100.

	:requestheader Authorization: данные, необходимые для :doc:`авторизации <../Authorization>`.

	:statuscode 200: операция успешно завершена.
	:statuscode 400: данные в запросе имеют неверный формат или отсутствуют обязательные параметры.
	:statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization`` или в этом заголовке содержатся некорректные авторизационные данные.
	:statuscode 402: у организации с указанным идентификатором ``boxId`` закончилась подписка на API.
	:statuscode 403: доступ к ящику с предоставленным авторизационным токеном запрещен или запрос сделан не от имени администратора.
	:statuscode 404: не найдена группа контрагентов с идентификатором ``CounteragentGroupId``.
	:statuscode 405: используется неподходящий HTTP-метод.
	:statuscode 500: при обработке запроса возникла непредвиденная ошибка.

	:response Body: Тело ответа содержит структуру ``CounteragentFromGroupResponse``:

		.. code-block:: protobuf

		    message CounteragentFromGroupResponse { 
		        repeated string CounteragentBoxId = 1;
		        required int32 TotalCount = 2;
		        optional string AfterIndexKey = 3;
		    }

		- ``CounteragentBoxId`` — список идентификаторов ящиков контрагентов.
		- ``TotalCount`` — количество контрагентов в группе.
		- ``AfterIndexKey`` — ключ для постраничного получения списка контрагентов.

.. include:: ../include/accessMethod_required_admin_manageCounteragents.txt

Метод вернет только идентификаторы контрагентов со статусом ``CounteragentStatus = IsMyCounteragent``. Узнать статус контрагента можно с помощью метода :doc:`GetOrganizationsByInnList`.


Примеры использования
---------------------

**Пример HTTP-запроса:**

.. literalinclude:: ../include/getCounteragentsFromGroup_query.txt

**Пример тела ответа:**

.. literalinclude:: ../include/getCounteragentsFromGroup_resp.txt
	:language: json


----

.. rubric:: См. также

.. include:: ../include/seealso_method_counteragentgroup.txt