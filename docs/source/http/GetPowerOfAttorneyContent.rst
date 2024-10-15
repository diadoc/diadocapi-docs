GetPowerOfAttorneyContent
=========================

Метод ``GetPowerOfAttorneyContent`` возвращает содержимое файлов машиночитаемой доверенности (МЧД) и родительских МЧД.

Версии метода:
	- :ref:`GetPowerOfAttorneyContent_v2` — возвращает файлы передоверенной МЧД и родительских МЧД.
	- :ref:`GetPowerOfAttorneyContent_v1` — метод устарел.
	
.. _GetPowerOfAttorneyContent_v2:

v2
--

.. http:get:: /V2/GetPowerOfAttorneyContent

	:queryparam boxId: идентификатор :doc:`ящика <../entities/box>` организации.
	:queryparam messageid: идентификатор сообщения.
	:queryparam entityid: идентификатор МЧД.

	:requestheader Authorization: данные, необходимые для :doc:`авторизации <../Authorization>`.

	:statuscode 200: операция успешно завершена.
	:statuscode 400: данные в запросе имеют неверный формат или отсутствуют обязательные параметры.
	:statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization`` или в этом заголовке содержатся некорректные авторизационные данные.
	:statuscode 402: у организации с указанным идентификатором ``boxId`` закончилась подписка на API.
	:statuscode 403: доступ к ящику с предоставленным авторизационным токеном запрещен.
	:statuscode 404: в указанном ящике нет сообщения с идентификатором ``messageId`` или в указанном сообщении нет сущности с идентификатором ``entityId``, или у указанной сущности нет содержимого, или не удалось получить XML-файл МЧД с электронной подписью от сервиса ФНС.
	:statuscode 405: используется неподходящий HTTP-метод.
	:statuscode 500: при обработке запроса возникла непредвиденная ошибка.

	:response Body: Тело ответа содержит структуру ``PowerOfAttorneyContentResponse``:

		.. code-block:: protobuf

		    message PowerOfAttorneyContentResponse {
		        required PowerOfAttorneyContentV2 Content = 1;
		        repeated PowerOfAttorneyContentV2 DelegationChain = 2;
		    }

		    message PowerOfAttorneyContentV2 {
		        required bytes Content = 1;
		        required bytes Signature = 2;
		        required PowerOfAttorneyFullId FullId = 3;
		    }

		..

		- ``Content`` — содержимое файла МЧД. Представлено структурой ``PowerOfAttorneyContentV2`` с полями:

			- ``Content`` — содержимое файла МЧД
			- ``Signature`` — подпись под МЧД.
			- ``PowerOfAttorneyFullId`` — идентификатор МЧД. Представлен структурой :doc:`../proto/PowerOfAttorneyFullId`.

		- ``DelegationChain`` — список предыдущих МЧД для доверенности, выпущенной в порядке передоверия. Каждая МЧД представлена структурой ``PowerOfAttorneyContentV2``. Список хранится в порядке от корневой МЧД (элемент с индексом ``0``) к дочерней, сама конечная МЧД в список не включена. Если предыдущих МЧД нет, то вернется пустой список. Заполняется только в случаях:

			- если при отправке документов в поле ``Contents`` структуры :doc:`../proto/PowerOfAttorneyToPost` была указана цепочка файлов МЧД;
			- если по идентификатору ``FullId`` удалось получить цепочку доверенностей из сервиса ФНС.

.. _GetPowerOfAttorneyContent_v1:

v1
--

.. http:get:: /GetPowerOfAttorneyContent

	:queryparam boxId: идентификатор :doc:`ящика <../entities/box>` организации.
	:queryparam messageid: идентификатор сообщения.
	:queryparam entityid: идентификатор МЧД.

	:requestheader Authorization: данные, необходимые для :doc:`авторизации <../Authorization>`.

	:statuscode 200: операция успешно завершена.
	:statuscode 400: данные в запросе имеют неверный формат или отсутствуют обязательные параметры.
	:statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization`` или в этом заголовке содержатся некорректные авторизационные данные.
	:statuscode 402: у организации с указанным идентификатором ``boxId`` закончилась подписка на API.
	:statuscode 403: доступ к ящику с предоставленным авторизационным токеном запрещен.
	:statuscode 404: в указанном ящике нет сообщения с идентификатором ``messageId`` или в указанном сообщении нет сущности с идентификатором ``entityId``, или у указанной сущности нет содержимого, или не удалось получить XML-файл МЧД с электронной подписью от сервиса ФНС.
	:statuscode 405: используется неподходящий HTTP-метод.
	:statuscode 500: при обработке запроса возникла непредвиденная ошибка.

	:response Body: Тело ответа содержит структуру ``PowerOfAttorneyContent``:

		.. code-block:: protobuf

		    message PowerOfAttorneyContent {
		        required bytes Content = 1;
		        required bytes Signature = 2;
		    }

		..

		- ``Content`` — содержимое файла МЧД.
		- ``Signature`` — подпись под МЧД.

----

.. rubric:: См. также

.. include:: ../include/seealso_method_powerofattorney.txt