GetWorkflowsSettings
====================

Метод ``GetWorkflowsSettings`` возвращает свойства указанного вида документооборота :doc:`../proto/DocumentWorkflow`.

.. http:get:: /GetWorkflowsSettings

	:queryparam boxId: идентификатор ящика организации.

	:requestheader Authorization: необходимые данные для :doc:`авторизации <../Authorization>`.

	:statuscode 200: операция успешно завершена
	:statuscode 400: данные в запросе имеют неверный формат или отсутствуют обязательные параметры
	:statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization`` или в этом заголовке содержатся некорректные авторизационные данные
	:statuscode 402: закончилась подписка на API
	:statuscode 403: доступ к ящику с предоставленным авторизационным токеном запрещен
	:statuscode 404: не найден ящик с указанным идентификатором
	:statuscode 500: при обработке запроса возникла непредвиденная ошибка

**Тело ответа:**  Метод возвращает структуру :doc:`../proto/DocumentWorkflowSettings`.
