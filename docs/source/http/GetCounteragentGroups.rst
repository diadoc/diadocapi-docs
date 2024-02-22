GetCounteragentGroups
=====================

Метод ``GetCounteragentGroups`` возвращает список групп контрагентов.

.. http:get:: /GetCounteragentGroups

	:queryparam boxId: идентификатор ящика организации.
	:queryparam offset: номер страницы, которую нужно получить. Необязательный параметр. По умолчанию равен 1.
	:queryparam limit: количество групп контрагентов на одной странице, максимальное значение для одной страницы. Может принимать значение от 1 до 100. Необязательный параметр, по умолчанию равен 100.

	:requestheader Authorization: данные, необходимые для :doc:`авторизации <../Authorization>`.

	:request Body: Тело запроса может отсутствовать или содержать структуру ``CounteragentGroupList``:

		.. code-block:: protobuf

		    message CounteragentGroupList {
		        repeated string CounteragentGroupId = 1;
		    }

		- ``CounteragentGroupId`` — список идентификаторов групп контрагентов.
	
	:statuscode 200: операция успешно завершена.
	:statuscode 400: данные в запросе имеют неверный формат или отсутствуют обязательные параметры, или невозможно изменить наименование группы по умолчанию.
	:statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization`` или в этом заголовке содержатся некорректные авторизационные данные.
	:statuscode 402: у организации с указанным идентификатором ``boxId`` закончилась подписка на API.
	:statuscode 405: используется неподходящий HTTP-метод.
	:statuscode 500: при обработке запроса возникла непредвиденная ошибка.

	:response Body: Тело ответа содержит структуру ``CounteragentGroupsResponse``:

		.. code-block:: protobuf

		    message CounteragentGroupsResponse { 
		        repeated CounteragentGroup Group = 1;
		        required int32 TotalCount = 2;
		    }

		- ``Group`` — список групп контрагентов. Каждый элемент списка представлен структурой :doc:`../proto/CounteragentGroup`.
		- ``TotalCount`` — количество групп контрагентов.

Для выполнения метода текущий пользователь должен иметь доступ к ящику.

Если тело запроса отсутствует, метод вернет полный список групп контрагентов.

Метод не возвращает удаленные группы контрагентов.

----

.. rubric:: Смотри также

*Другие методы для работы с группой контрагентов:*
	- :doc:`CreateCounteragentGroup` — создает группу контрагентов,
	- :doc:`UpdateCounteragentGroup` — редактирует группы контрагентов,
	- :doc:`DeleteCounteragentGroup` — удаляет группу контрагентов,
	- :doc:`AddCounteragentsInGroup` — добавляет контрагентов в группу,
	- :doc:`GetCounteragentsInGroup` — возвращает список контрагентов в группе.

