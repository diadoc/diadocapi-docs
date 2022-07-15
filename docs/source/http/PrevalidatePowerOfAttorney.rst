PrevalidatePowerOfAttorney
==========================

Метод ``PrevalidatePowerOfAttorney`` выполняет предварительную проверку машиночитаемой доверенности (МЧД).

В рамках метода выполняется проверка следующих параметров:

	- доверенность действующая: проверка выполняется на основании дат действия доверенности, отзыв МЧД может быть не учтен;
	- представитель в МЧД соответствует субъекту из сертификата электронной подписи.

.. http:post:: /PrevalidatePowerOfAttorney

	:queryparam boxId: идентификатор ящика организации.
	:queryparam registrationNumber: регистрационный номер МЧД.
	:queryparam issuerInn: ИНН доверителя.

	:requestheader Authorization: данные, необходимые для :doc:`авторизации <../Authorization>`.

	:request Body: Тело запроса должно содержать данные для проверки МЧД, представленные структурой :doc:`../proto/PowerOfAttorneyPrevalidateRequest`.

	:statuscode 200: операция успешно завершена.
	:statuscode 400: данные в запросе имеют неверный формат или отсутствуют обязательные параметры.
	:statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization`` или в этом заголовке содержатся некорректные авторизационные данные.
	:statuscode 402: у организации с указанным идентификатором ``boxId`` закончилась подписка на API.
	:statuscode 403: доступ к ящику с предоставленным авторизационным токеном запрещен.
	:statuscode 404: не найден ящик с указанным идентификатором или не найдена МЧД для сотрудника.
	:statuscode 405: используется неподходящий HTTP-метод.
	:statuscode 500: при обработке запроса возникла непредвиденная ошибка.

Метод возвращает результат проверки МЧД, представленный структурой ``PowerOfAttorneyPrevalidateResult``.

.. code-block:: protobuf

    message PowerOfAttorneyPrevalidateResult {
        required PowerOfAttorneyValidationStatus PrevalidateStatus = 1;
    }

- ``PrevalidateStatus`` — статус проверки, представленный структурой :doc:`../proto/PowerOfAttorneyValidationStatus`.