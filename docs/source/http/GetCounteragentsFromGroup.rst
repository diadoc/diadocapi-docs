GetCounteragentsFromGroup
=========================

Метод ``GetCounteragentsFromGroup`` возращает список контрагентов в группе.

.. http:get:: /GetCounteragentsFromGroup

	:queryparam boxId: идентификатор ящика организации.
	:queryparam counteragentGroupId: идентификатор группы контрагентов
	:queryparam afterIndexKey: уникальный ключ, позволяющий итерироваться по списку контрагентов. Необязательный параметр.
	:queryparam count: максимальное количество контрагентов в ответе. Может принимать значения от 1 до 100. Необязательный параметр. По умолчанию равен 100.

	:requestheader Authorization: данные, необходимые для :doc:`авторизации <../Authorization>`.

	:statuscode 200: операция успешно завершена.
	:statuscode 400: данные в запросе имеют неверный формат или отсутствуют обязательные параметры, или невозможно изменить наименование группы по умолчанию.
	:statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization`` или в этом заголовке содержатся некорректные авторизационные данные.
	:statuscode 402: у организации с указанным идентификатором ``boxId`` закончилась подписка на API.
	:statuscode 404: не найдена группа контрагентов с идентификатором ``CounteragentGroupId``.
	:statuscode 405: используется неподходящий HTTP-метод.
	:statuscode 409: с контрагентом не установлены партнерские отношения.
	:statuscode 500: при обработке запроса возникла непредвиденная ошибка.

	:response Body: Тело ответа содержит структуру ``CounteragentFromGroupResponse``:

		.. code-block:: protobuf

		    message CounteragentFromGroupResponse { 
		        repeated string CounteragentBoxId = 1;
		        required int32 TotalCount = 2;
		        optional string AfterIndexKey = 3;
		    }

		- ``CounteragentId`` — список идентификаторов ящиков контрагентов.
		- ``TotalCount`` — количество контрагентов в группе.
		- ``AfterIndexKey`` — ключ для постраничного получения списка контрагентов.

Получить список контрагентов в группе может только администратор ящика с разрешением ``CanManageCounteragents``, позволяющим видеть списки контрагентов и работать с ними.

Метод вернет идентификатор контрагента ``CounteragentId``, если статус контрагента ``CounteragentStatus = IsMyCounteragent``. Узнать статус можно с помощью метода :doc:`GetOrganizationsByInnList`.

----

.. rubric:: Смотри также

*Другие методы для работы с группой контрагентов:*
	- :doc:`CreateCounteragentGroup` — создает группу контрагентов,
	- :doc:`UpdateCounteragentGroup` — редактирует группы контрагентов,
	- :doc:`DeleteCounteragentGroup` — удаляет группу контрагентов,
	- :doc:`AddCounteragentToGroup` — возращает список групп контрагентов,
	- :doc:`GetCounteragentGroups` — возвращает список контрагентов в группе,
	- :doc:`GetCounteragentGroup` — возвращает информацию о группе контрагентов.