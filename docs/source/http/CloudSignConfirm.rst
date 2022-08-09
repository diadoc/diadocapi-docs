CloudSignConfirm
================

Метод ``CloudSignConfirm`` предназначен для передачи СМС-кода подтверждения операции подписания Контур.Сертификатом. Метод является асинхронным, чтобы завершить операцию используйте метод :doc:`CloudSignConfirmResult`.

.. http:post:: /CloudSignConfirm

	:queryparam token: идентификатор операции подписания Контур.Сертификатом. Результат вызова пары методов :doc:`CloudSign` и :doc:`CloudSignResult`.
	:queryparam confirmationCode: СМС-код подтверждения операции подписания Контур.Сертификатом.
	:queryparam locationPreference: способ, которым вернется результат подписания. Может принимать значения:
								- ``Content`` — байтовое представление. Является значением по умолчанию.
								- ``Reference`` — путь на полке. Подробнее про полку в описании метода :doc:`ShelfUpload`

	:requestheader Authorization: данные, необходимые для :doc:`авторизации <../Authorization>`.

	:statuscode 200: операция успешно завершена.
	:statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization``, или в этом заголовке отсутствует параметр ``ddauth_api_client_id``, или переданный в нем ключ разработчика не зарегистрирован в Диадоке.
	:statuscode 405: используется неподходящий HTTP-метод.
	:statuscode 409: зависит от значения заголовка ``X-Diadoc-ErrorCode``:
					- ``CloudCrypt.BadConfirmationCode`` - указан неверный код подтверждения,
					- ``CloudCrypt.ExpiredRequest`` - истек срок действия кода подтверждения.
	:statuscode 500: при обработке запроса возникла непредвиденная ошибка.


    :response Body: Тело ответа содержит идентификатор операции ``taskId`` в структуре :doc:`../proto/AsyncMethodResult`. По этому идентификатору с помощью метода :doc:`CloudSignConfirmResult` можно узнать результат обработки запроса.

----

.. rubric:: Смотри также

- :doc:`http/CloudSign`
- :doc:`http/CloudSignResult`
- :doc:`http/CloudSignConfirmResult`
