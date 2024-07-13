﻿GetDocumentTypes
================

Метод ``GetDocumentTypes`` возвращает описание типов документов, доступных в ящике.

.. http:get:: /V2/GetDocumentTypes

	:queryparam boxId: идентификатор :doc:`ящика <../entities/box>` организации.

	:requestheader Authorization: данные, необходимые для :doc:`авторизации <../Authorization>`.

	:statuscode 200: операция успешно завершена.
	:statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization`` или в этом заголовке содержатся некорректные авторизационные данные.
	:statuscode 402: у организации с указанным идентификатором ``boxId`` закончилась подписка на API.
	:statuscode 403: доступ к ящику с предоставленным авторизационным токеном запрещен.
	:statuscode 405: используется неподходящий HTTP-метод.
	:statuscode 500: при обработке запроса возникла непредвиденная ошибка.

	:response Body: Тело ответа содержит структуру ``GetDocumentTypesResponseV2`` с описанием типов документов:

		.. code-block:: protobuf

		    message GetDocumentTypesResponseV2 {
		        repeated DocumentTypeDescriptionV2 DocumentTypes = 1;
		    }

		..

		- ``DocumentTypes`` — список типов документов, представленных структурой :doc:`../proto/DocumentTypeDescriptionV2`.
		
Инструкция о получении данных из метода ``GetDocumentTypes`` приведена на странице :doc:`../instructions/getdoctypes`.


----

.. rubric:: См. также

*Инструкции:*
	- :doc:`../instructions/getdoctypes`