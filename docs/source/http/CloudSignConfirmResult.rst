CloudSignConfirmResult
======================

Метод ``CloudSignConfirmResult`` предназначен для получения готовых подписей или информации об ошибке. Парный метод к асинхронному методу :doc:`CloudSignConfirm`.

.. http:get:: /CloudSignConfirmResult

	:queryparam taskId: идентификатор асинхронного вызова, полученный методом :doc:`CloudSignConfirm`.

	:requestheader Authorization: данные, необходимые для :doc:`авторизации <../Authorization>`.

	:statuscode 200: операция успешно завершена.
	:statuscode 204: операция еще не завершена. В HTTP-заголовке ответа ``Retry-After`` в секундах указывается время, через которое нужно повторить запрос.
	:statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization`` или в этом заголовке содержатся некорректные авторизационные данные.
	:statuscode 405: используется неподходящий HTTP-метод.
	:statuscode 500: при обработке запроса возникла непредвиденная ошибка.

	:responseheader Retry-After: если в ответе содержится HTTP-заголовок ``Retry-After``, то предыдущий вызов этого метода с таким же идентификатором операции еще не завершен. В этом случае следует повторить вызов через указанное в заголовке время (в секундах), чтобы убедиться, что операция завершилась без ошибок.

	:response body: Тело ответа содержит результат выполнения операции, представленный структурой :doc:`CloudSignConfirmResult <../proto/CloudSignConfirmResultDTO>`.

----

.. rubric:: Смотри также

*Методы для работы с Контур.Сертификатом:*
	- :doc:`CloudSign`
	- :doc:`CloudSignResult`
	- :doc:`CloudSignConfirm`