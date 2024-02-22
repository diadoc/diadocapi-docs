AddCounteragentsInGroup
=======================

Метод ``AddCounteragentsInGroup`` добавляет контрагентов в группу.

.. http:get:: /AddCounteragentsInGroup

	:queryparam boxId: идентификатор ящика организации.
	:queryparam CounteragentGroupId: идентификатор группы контрагентов.

	:requestheader Authorization: данные, необходимые для :doc:`авторизации <../Authorization>`.

	:request Body: Тело запроса должно содержать структуру  ``CounteragentsInGroupToAdd``:

		.. code-block:: protobuf

		    message CounteragentsInGroupToAdd {
		        repeated boxid = 1;
		    }

		..

		- ``boxid`` — список идентификаторов ящиков контрагентов.

	:statuscode 200: операция успешно завершена.
	:statuscode 400: данные в запросе имеют неверный формат или отсутствуют обязательные параметры, или невозможно изменить наименование группы по умолчанию.
	:statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization`` или в этом заголовке содержатся некорректные авторизационные данные.
	:statuscode 402: у организации с указанным идентификатором ``boxId`` закончилась подписка на API.
	:statuscode 403: доступ к ящику с предоставленным авторизационным токеном запрещен или запрос сделан не от имени администратора.
	:statuscode 404: не найдена группа контрагентов с идентификатором ``CounteragentGroupId``.
	:statuscode 405: используется неподходящий HTTP-метод.
	:statuscode 500: при обработке запроса возникла непредвиденная ошибка.

	:response Body: Тело ответа содержит структуру ``CounteragentsInGroupPatchResponse``:

		.. code-block:: protobuf

		    message CounteragentsInGroupPatchResponse { 
		    repeated CounteragentInGroupStatus CounteragentInGroup = 1;
		    }
		
		    message CounteragentInGroupStatus {
		        required string boxId = 1;
		        required bool Status = 2;
		        optional string Reason = 3;
		    }

		- ``CounteragentInGroup`` — список контрагентов в группе. Каждый элемент списка представлен структурой ``CounteragentInGroupStatus`` с полями:

			- ``boxId`` — идентификатор ящика контрагента.
			- ``Status`` — флаг, указывающий что контрагент добавлен в группу.
			- ``Reason`` — причина, по которой контрагент не добавлен в группу. Возвращается, если ``Status = false``.

Добавить контрагентов в группу может только администратор ящика.

Метод ``AddCounteragentsInGroup`` добавляет в группу только контрагентов со статусом ``CounteragentStatus = IsMyCounteragent``. Иначе в поле ``Reason`` метод вернет сообщение «Контрагент не является партнером, назначить группу невозможно».

Узнать статус контрагента можно с помощью метода :doc:`GetOrganizationsByInnList`.

----

.. rubric:: Смотри также

*Другие методы для работы с группой контрагентов:*
	- :doc:`CreateCounteragentGroup` — создает группу контрагентов,
	- :doc:`UpdateCounteragentGroup` — редактирует группы контрагентов,
	- :doc:`DeleteCounteragentGroup` — удаляет группу контрагентов,
	- :doc:`GetCounteragentGroups` — возвращает список групп контрагентов,
	- :doc:`GetCounteragentsInGroup` — возвращает список контрагентов в группе.