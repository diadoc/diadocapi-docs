RegisterPowerOfAttorney
=======================

Метод ``RegisterPowerOfAttorney`` отправляет запрос на регистрацию машиночитаемой доверенности (МЧД).

.. http:post:: /RegisterPowerOfAttorney

	:queryparam boxId: идентификатор :doc:`ящика <../entities/box>` организации.

	:requestheader Authorization: данные, необходимые для :doc:`авторизации <../Authorization>`.

	:request Body: Тело запроса должно содержать данные для регистрации МЧД, представленные структурой :doc:`../proto/PowerOfAttorneyToRegister`.

	:statuscode 200: операция успешно завершена.
	:statuscode 400: данные в запросе имеют неверный формат или отсутствуют обязательные параметры.
	:statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization`` или в этом заголовке содержатся некорректные авторизационные данные.
	:statuscode 402: у организации с указанным идентификатором ``boxId`` закончилась подписка на API.
	:statuscode 403: доступ к ящику с предоставленным авторизационным токеном запрещен.
	:statuscode 404: не найден ящик с указанным идентификатором.
	:statuscode 405: используется неподходящий HTTP-метод.
	:statuscode 409: не удалось выполнить запрос на регистрацию.
	:statuscode 500: при обработке запроса возникла непредвиденная ошибка.

	:response Body: Тело ответа содержит идентификатор операции ``taskId`` в структуре :doc:`../proto/AsyncMethodResult`. По этому идентификатору с помощью метода :doc:`RegisterPowerOfAttorneyResult` можно узнать результат обработки запроса.

----

.. rubric:: См. также

*Руководства:*
	- :doc:`../howto/powerofattorney`

*Другие методы для работы с МЧД:*
	- :doc:`AddEmployeePowerOfAttorney` — привязывает МЧД к сотруднику
	- :doc:`DeleteEmployeePowerOfAttorney` — отвязывает МЧД от сотрудника
	- :doc:`GetEmployeePowersOfAttorney` — возвращает МЧД, привязанные к сотруднику
	- :doc:`GetPowerOfAttorneyContent` — возвращает содержимое файлов МЧД и родительских МЧД
	- :doc:`GetPowerOfAttorneyInfo` — возвращает информацию о МЧД, отправленной с документом
	- :doc:`PrevalidatePowerOfAttorney` — выполняет предварительную проверку МЧД
	- :doc:`RegisterPowerOfAttorneyResult` — возвращает результат регистрации МЧД
	- :doc:`UpdateEmployeePowerOfAttorney` — изменяет параметр МЧД «Использовать по умолчанию»