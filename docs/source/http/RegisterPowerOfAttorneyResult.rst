RegisterPowerOfAttorneyResult
=============================

Метод ``RegisterPowerOfAttorneyResult`` возвращает результат регистрации машиночитаемой доверенности (МЧД), выполняемой методом :doc:`RegisterPowerOfAttorney`.

.. http:get:: /RegisterPowerOfAttorneyResult

	:queryparam boxId: идентификатор ящика организации.
	:queryparam taskId: идентификатор операции, полученный методом :doc:`RegisterPowerOfAttorney`.

	:requestheader Authorization: данные, необходимые для :doc:`авторизации <../Authorization>`.

	:statuscode 200: операция успешно завершена.
	:statuscode 400: данные в запросе имеют неверный формат или отсутствуют обязательные параметры.
	:statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization`` или в этом заголовке содержатся некорректные авторизационные данные.
	:statuscode 402: у организации с указанным идентификатором ``boxId`` закончилась подписка на API.
	:statuscode 403: доступ к ящику с предоставленным авторизационным токеном запрещен или запрос выполнен не от имени администратора или пользователя, для которого нужно зарегистрировать МЧД.
	:statuscode 404: не найден ящик с указанным идентификатором или неизвестный ``taskId``.
	:statuscode 405: используется неподходящий HTTP-метод.
	:statuscode 500: при обработке запроса возникла непредвиденная ошибка.

	:response Body: Тело ответа содержит результат регистрации МЧД, представленный структурой :doc:`../proto/PowerOfAttorneyRegisterResult`.

Если МЧД уже была зарегистрирована раньше, то метод вернет код ``200 (OK)`` и заполненную структуру :doc:`../proto/PowerOfAttorney` внутри тела ответа.

----

.. rubric:: Смотри также

*Руководства:*
	- :doc:`Как работать с МЧД <../howto/powerofattorney>`

*Другие методы для работы с МЧД:*
	- :doc:`RegisterPowerOfAttorney` — отправляет запрос на регистрацию МЧД.
	- :doc:`GetEmployeePowersOfAttorney` — возвращает МЧД, привязанные к сотруднику.
	- :doc:`AddEmployeePowerOfAttorney` — привязывает МЧД к сотруднику.
	- :doc:`DeleteEmployeePowerOfAttorney` — отвязывает МЧД от сотрудника.
	- :doc:`UpdateEmployeePowerOfAttorney` — изменяет параметр МЧД «Использовать по умолчанию».
	- :doc:`PrevalidatePowerOfAttorney` — выполняет предварительную проверку МЧД.
	- :doc:`GetPowerOfAttorneyInfo` — возвращает информацию о МЧД, отправленной с документом.