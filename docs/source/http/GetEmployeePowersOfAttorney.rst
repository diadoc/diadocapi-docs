GetEmployeePowersOfAttorney
===========================

Метод ``GetEmployeePowersOfAttorney`` возвращает машиночитаемые доверенности (МЧД), привязанные к сотруднику: как действующие, так и истекшие.

.. http:get:: /GetEmployeePowersOfAttorney

	:queryparam boxId: идентификатор ящика организации.
	:queryparam userId: идентификатор сотрудника. Если не указан, то метод вернет МЧД пользователя, от имени которого вызывается метод.
	:queryparam onlyActual: признак того, что нужно возвращать только действующие МЧД. По умолчанию имеет значение ``false``.

	:requestheader Authorization: данные, необходимые для :doc:`авторизации <../Authorization>`.

	:statuscode 200: операция успешно завершена.
	:statuscode 400: данные в запросе имеют неверный формат или отсутствуют обязательные параметры.
	:statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization`` или в этом заголовке содержатся некорректные авторизационные данные.
	:statuscode 402: у организации с указанным идентификатором ``boxId`` закончилась подписка на API.
	:statuscode 403: доступ к ящику с предоставленным авторизационным токеном запрещен или запрос выполнен не от имени администратора или пользователя, для которого необходимо получить МЧД.
	:statuscode 404: не найден ящик или пользователь с указанными идентификаторами или не найден сотрудник в ящике для данного пользователя.
	:statuscode 405: используется неподходящий HTTP-метод.
	:statuscode 500: при обработке запроса возникла непредвиденная ошибка.

	:response Body: Тело ответа содержит список МЧД, представленный структурой ``EmployeePowerOfAttorneyList``:

		.. code-block:: protobuf

			message EmployeePowerOfAttorneyList {
				repeated EmployeePowerOfAttorney PowersOfAttorney = 1;
			}
			
		..

		- ``PowersOfAttorney`` —  список МЧД, привязанных к сотруднику, представленных структурой :doc:`../proto/EmployeePowerOfAttorney`.

Получить МЧД сотрудника может он сам или администратор ящика.

Если у сотрудника нет привязанных МЧД, то метод вернет код ``200 (OK)`` и пустой список ``PowersOfAttorney``.

----

Смотри также
^^^^^^^^^^^^

Инструкции:
	- :doc:`Как работать с МЧД <../howto/powerofattorney>`

Другие методы для работы с МЧД:
	- :doc:`RegisterPowerOfAttorney` — отправляет запрос на регистрацию МЧД.
	- :doc:`RegisterPowerOfAttorneyResult` — возвращает результат регистрации МЧД.
	- :doc:`AddEmployeePowerOfAttorney` — привязывает МЧД к сотруднику.
	- :doc:`DeleteEmployeePowerOfAttorney` — отвязывает МЧД от сотрудника.
	- :doc:`UpdateEmployeePowerOfAttorney` — изменяет параметр МЧД «Использовать по умолчанию».
	- :doc:`PrevalidatePowerOfAttorney` — выполняет предварительную проверку МЧД.
	- :doc:`GetPowerOfAttorneyInfo` — возвращает информацию о МЧД, отправленной с документом.