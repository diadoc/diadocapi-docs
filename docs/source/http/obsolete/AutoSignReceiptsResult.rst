AutoSignReceiptsResult
=======================

.. warning::
	Метод устарел.

Метод ``AutoSignReceiptsResult`` возвращает состояние задачи на подписание уведомлений, ранее запущенной методом :doc:`AutoSignReceipts`.

.. http:get:: /AutoSignReceiptsResult

	:queryparam taskId: идентификатор операции, полученный методом :doc:`AutoSignReceipts`.

	:requestheader Authorization: данные, необходимые для :doc:`авторизации <../../Authorization>`.

	:statuscode 200: операция успешно завершена.
	:statuscode 204: операция еще не завершена. В HTTP-заголовке ответа ``Retry-After`` указано время в секундах, через которое нужно повторить запрос.
	:statuscode 400: данные в запросе имеют неверный формат или отсутствуют обязательные параметры.
	:statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization`` или в этом заголовке содержатся некорректные авторизационные данные.
	:statuscode 403: доступ к ящику с предоставленным авторизационным токеном запрещен.
	:statuscode 404: не найден ящик с указанным идентификатором.
	:statuscode 405: используется неподходящий HTTP-метод.
	:statuscode 500: при обработке запроса возникла непредвиденная ошибка.

	:response Body: Тело ответа содержит результат выполнения операции, представленный структурой :doc:`../../proto/obsolete/AutosignReceiptsResult`.
