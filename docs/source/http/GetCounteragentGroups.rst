GetCounteragentGroups
=====================

Метод ``GetCounteragentGroups`` возвращает список групп контрагентов указанной организации.

.. http:get:: /GetCounteragentGroups

	:queryparam boxId: идентификатор :doc:`ящика <../../entities/box>` организации.
	:queryparam page: номер страницы, которую нужно получить. Необязательный параметр. По умолчанию равен 1.
	:queryparam count: количество групп контрагентов на одной странице. Может принимать значение от 1 до 50. Необязательный параметр. По умолчанию равен 50.

	:requestheader Authorization: данные, необходимые для :doc:`авторизации <../Authorization>`.

	:statuscode 200: операция успешно завершена.
	:statuscode 400: данные в запросе имеют неверный формат или отсутствуют обязательные параметры.
	:statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization`` или в этом заголовке содержатся некорректные авторизационные данные.
	:statuscode 402: у организации с указанным идентификатором ``boxId`` закончилась подписка на API.
	:statuscode 403: доступ к ящику с предоставленным авторизационным токеном запрещен или запрос сделан не от имени сотрудника организации с разрешением ``CanManageCounteragents``.
	:statuscode 405: используется неподходящий HTTP-метод.
	:statuscode 500: при обработке запроса возникла непредвиденная ошибка.

	:response Body: Тело ответа содержит структуру ``CounteragentGroupsList``:

		.. code-block:: protobuf

		    message CounteragentGroupsList { 
		        repeated CounteragentGroup Groups = 1;
		        required int32 TotalCount = 2;
		    }

		- ``Groups`` — список групп контрагентов. Каждый элемент списка представлен структурой :doc:`../proto/CounteragentGroup`.
		- ``TotalCount`` — количество групп контрагентов.

Получить список групп контрагентов может только сотрудник организации с разрешением ``CanManageCounteragents``, позволяющим видеть списки контрагентов и работать с ними.

Метод не возвращает удаленные группы контрагентов.

----

.. rubric:: См. также

.. include:: ../reused_text/counteragentgroup_seealso.txt