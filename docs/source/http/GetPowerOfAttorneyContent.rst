GetPowerOfAttorneyContent
=========================

Метод ``GetPowerOfAttorneyContent`` возвращает содержимое файла машиночитаемой доверенности (МЧД) и подпись под ней.

.. http:get:: /GetPowerOfAttorneyContent

	:queryparam boxid: идентификатор ящика организации.
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
		        requires bytes Signature = 2;
		    }

		..

		- ``Content`` — содержимое файла МЧД.
		- ``Signature`` — подпись под МЧД.

----

.. rubric:: Смотри также

*Руководства:*
	- :doc:`Как работать с МЧД <../howto/powerofattorney>`

*Другие методы для работы с МЧД:*
	- :doc:`RegisterPowerOfAttorney` — отправляет запрос на регистрацию МЧД.
	- :doc:`RegisterPowerOfAttorneyResult` — возвращает результат регистрации МЧД.
	- :doc:`GetEmployeePowersOfAttorney` — возвращает МЧД, привязанные к сотруднику.
	- :doc:`AddEmployeePowerOfAttorney` — привязывает МЧД к сотруднику.
	- :doc:`DeleteEmployeePowerOfAttorney` — отвязывает МЧД от сотрудника.
	- :doc:`UpdateEmployeePowerOfAttorney` — изменяет параметр МЧД «Использовать по умолчанию».
	- :doc:`PrevalidatePowerOfAttorney` — выполняет предварительную проверку МЧД.