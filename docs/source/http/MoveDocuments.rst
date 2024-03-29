MoveDocuments
=============

Метод ``MoveDocuments`` перемещает документы в подразделение организации.

.. http:post:: /MoveDocuments

	:requestheader Authorization: данные, необходимые для :doc:`авторизации <../Authorization>`.
	
	:request Body: Тело запроса должно содержать структуру :doc:`../proto/DocumentsMoveOperation`.

	:statuscode 200: операция успешно завершена.
	:statuscode 400: данные в запросе имеют неверный формат или отсутствуют обязательные параметры.
	:statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization`` или в этом заголовке содержатся некорректные авторизационные данные.
	:statuscode 402: у организации с указанным идентификатором ``boxId`` закончилась подписка на API.
	:statuscode 403: доступ к ящику с предоставленным авторизационным токеном запрещен.
	:statuscode 405: используется неподходящий HTTP-метод.
	:statuscode 500: при обработке запроса возникла непредвиденная ошибка.
	
Для выполнения метода текущий пользователь должен иметь доступ ко всем перемещаемым документам, иначе метод вернет ошибку ``403 (Forbidden)``.