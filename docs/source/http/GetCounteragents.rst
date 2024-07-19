GetCounteragents
================

Метод ``GetCounteragents`` осуществляет поиск :doc:`контрагентов <../entities/counteragent>` по указанным параметрам.

.. http:get:: /V3/GetCounteragents

	:queryparam myBoxId: идентификатор :doc:`ящика <../../entities/box>` организации, для которой осуществляется поиск контрагентов.
	:queryparam counteragentStatus: статус контрагента. Необязательный параметр, используется для фильтрации результатов поиска.
	:queryparam afterIndexKey: уникальный ключ для постраничного получения списка контрагентов, удовлетворяющих фильтру. Необязательный параметр.
	:queryparam query: текстовая строка для поиска организации по краткому или полному наименованию ящика контрагента или ИНН. Нельзя указывать одновременно с ``afterIndexKey``.

	:requestheader Authorization: данные, необходимые для :doc:`авторизации <../Authorization>`.
	
	:statuscode 200: операция успешно завершена.
	:statuscode 400: данные в запросе имеют неверный формат или отсутствуют обязательные параметры.
	:statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization`` или в этом заголовке содержатся некорректные авторизационные данные.
	:statuscode 402: у организации с указанным идентификатором ``myOrgId`` закончилась подписка на API.
	:statuscode 403: доступ к списку контрагентов организации ``myOrgId`` с предоставленным авторизационным токеном запрещен.
	:statuscode 405: используется неподходящий HTTP-метод.
	:statuscode 500: при обработке запроса возникла непредвиденная ошибка.

	:response Body: Тело ответа содержит список контрагентов организации ``myOrgId``, находящихся в статусе ``counteragentStatus``. Список представлен структурой ``CounteragentList``:

		.. code-block:: protobuf

		    message CounteragentList {
		        required int32 TotalCount = 1;
		        repeated Counteragent Counteragents = 2;
		        required TotalCountType TotalCountType = 3;
		    }

		- ``TotalCount`` — количество контрагентов, удовлетворяющих запросу.
		- ``Counteragents`` — список контрагентов. Каждый элемент списка представлен структурой :doc:`../proto/Counteragent`.
		- ``TotalCountType`` — параметр, указывающий, является ли значение ``TotalCount`` точным или подсчет был ограничен максимальным количеством элементов в списке. Принимает значения из перечисления :doc:`../proto/TotalCountType`.

.. include:: ../include/accessMethod_required_box.txt

Список ``CounteragentList.Counteragents`` может содержать не более 100 элементов. Чтобы получить остальные элементы, вызовите метод ``GetCounteragents`` с теми же параметрами и дополнительно укажите параметр ``afterIndexKey``. В зависимости от значения параметра ``afterIndexKey`` метод работает следующим образом:

	- Если в запросе отсутствует параметр ``afterIndexKey``, метод вернет начало списка контрагентов, удовлетворяющих фильтру. Если в списке контрагентов меньше 100 элементов, метод вернет список полностью.
	- Если в запросе указан параметр ``afterIndexKey``, метод вернет список контрагентов, следующих за контрагентом с параметром ``afterIndexKey``. Контрагент с параметром ``afterIndexKey`` в этот список не попадает. Ключ контрагента указан в поле ``IndexKey`` структуры :doc:`../proto/Counteragent`.

Параметр ``counteragentStatus`` предназначен для фильтрации результатов поиска. Если параметр ``counteragentStatus`` не задан, метод вернет весь список контрагентов. Значения статусов контрагента описаны в перечислении :doc:`CounteragentStatus <../proto/Counteragent>`. В качестве параметра ``counteragentStatus`` можно передавать следующие значения:

	- ``IsMyCounteragent``,
	- ``InvitesMe``,
	- ``IsInvitedByMe``,
	- ``Rejected``.

Во вложенной структуре :doc:`Counteragent.Organization <../proto/Organization>` поле ``Departments`` будет пустым.


----

.. rubric:: См. также

.. include:: ../include/seealso_counteragents.txt

*Устаревшие версии метода:*
	- :doc:`obsolete/GetCounteragents`
	- :doc:`obsolete/GetCounteragents_v2`