GetWorkflowsSettings
====================

Метод ``GetWorkflowsSettings`` возвращает свойства всех :doc:`видов документооборота <../proto/DocumentWorkflow>`.

Версии метода:

	- :ref:`GetWorkflowsSettings V2 <GetWorkflowsSettings_v2>`.
	- :ref:`GetWorkflowsSettings <GetWorkflowsSettings_v1>` — устаревшая версия.

.. _GetWorkflowsSettings_v2:

GetWorkflowsSettings V2
-----------------------

.. http:get:: /V2/GetWorkflowsSettings

	:queryparam boxId: идентификатор :doc:`ящика <../entities/box>` организации.

	:requestheader Authorization: данные, необходимые для :doc:`авторизации <../Authorization>`.

	:statuscode 200: операция успешно завершена.
	:statuscode 400: данные в запросе имеют неверный формат или отсутствуют обязательные параметры.
	:statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization`` или в этом заголовке содержатся некорректные авторизационные данные.
	:statuscode 402: у организации с указанным идентификатором ``boxId`` закончилась подписка на API.
	:statuscode 403: доступ к ящику с предоставленным авторизационным токеном запрещен.
	:statuscode 404: не найден ящик с указанным идентификатором.
	:statuscode 500: при обработке запроса возникла непредвиденная ошибка.
	
	:response Body: Тело ответа содержит структуру :doc:`../proto/DocumentWorkflowSettingsV2` со свойствами вида документооборота.

.. _GetWorkflowsSettings_v1:

GetWorkflowsSettings
--------------------

.. http:get:: /GetWorkflowsSettings

	:queryparam boxId: идентификатор :doc:`ящика <../entities/box>` организации.

	:requestheader Authorization: данные, необходимые для :doc:`авторизации <../Authorization>`.

	:statuscode 200: операция успешно завершена.
	:statuscode 400: данные в запросе имеют неверный формат или отсутствуют обязательные параметры.
	:statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization`` или в этом заголовке содержатся некорректные авторизационные данные.
	:statuscode 402: у организации с указанным идентификатором ``boxId`` закончилась подписка на API.
	:statuscode 403: доступ к ящику с предоставленным авторизационным токеном запрещен.
	:statuscode 404: не найден ящик с указанным идентификатором.
	:statuscode 500: при обработке запроса возникла непредвиденная ошибка.
	
	:response Body: Тело ответа содержит коллекцию структур :doc:`../proto/obsolete/DocumentWorkflowSettings`, содержащих свойства вида документооборота.

----

.. rubric:: См. также

*Руководства:*
	- :doc:`../docflows/Workflows`