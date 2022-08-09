CloudSignConfirmResult
======================

Метод ``CloudSignConfirmResult`` предназначен для получения готовых подписей или информации об ошибке. Парный метод к асинхронному методу :doc:`CloudSignConfirm`.

.. http:get:: /CloudSignConfirmResult

    :queryparam taskId: идентификатор асинхронного вызова.

    :requestheader Authorization: данные, необходимые для :doc:`авторизации <../Authorization>`.

    :statuscode 200: операция успешно завершена.
    :statuscode 204: операция еще не завершена.
	:statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization``, или в этом заголовке отсутствует параметр ``ddauth_api_client_id``, или переданный в нем ключ разработчика не зарегистрирован в Диадоке.
	:statuscode 405: используется неподходящий HTTP-метод.
    :statuscode 500: при обработке запроса возникла непредвиденная ошибка.

    :response body: Тело ответа зависит от кода ответа:
                    - ``200 (OK)`` — в теле ответа содержится результат :doc:`CloudSignConfirmResult <../proto/CloudSignConfirmResultDTO>`.
                    - ``204 (No Content)`` — тело ответа пустое. В HTTP-заголовке ответа ``Retry-After`` в секундах указывается время, через которое нужно повторить запрос.


----

.. rubric:: Смотри также

- :doc:`http/CloudSign`
- :doc:`http/CloudSignResult`
- :doc:`http/CloudSignConfirm`