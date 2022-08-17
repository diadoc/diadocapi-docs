ForwardDocument
===============

Метод ``ForwardDocument`` пересылает документ в указанный ящик.

.. http:post:: /V2/ForwardDocument

	:queryparam boxId: идентификатор ящика организации.

	:requestheader Authorization: данные, необходимые для :doc:`авторизации <../Authorization>`.

	:request Body: Тело запроса должно содержать данные для пересылки документа, представленные структурой ``ForwardDocumentRequest``:

		.. code-block:: protobuf

			message ForwardDocumentRequest
			{
			    required string ToBoxId = 1;
			    required DocumentId DocumentId = 2;
			}

		..

		- ``ToBoxId`` — идентификатор ящика организации, в который нужно переслать документ.
		- ``DocumentId`` — идентификатор документа, который нужно переслать, представленный структурой :doc:`../proto/DocumentId`.

	:statuscode 200: операция успешно завершена.
	:statuscode 400: данные в запросе имеют неверный формат или отсутствуют обязательные параметры.
	:statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization`` или в этом заголовке содержатся некорректные авторизационные данные.
	:statuscode 402: у организации с указанным идентификатором ``boxId`` закончилась подписка на API.
	:statuscode 403: доступ к ящику с предоставленным авторизационным токеном запрещен.
	:statuscode 404: не найдено сообщение или документ с указанными идентификаторами.
	:statuscode 405: используется неподходящий HTTP-метод.
	:statuscode 409: текущее состояние системы не позволяет корректно обработать запрос или запрещен прием документов от контрагентов согласно свойству ``Sociability`` из :doc:`../proto/Organization`.
	:statuscode 500: при обработке запроса возникла непредвиденная ошибка.

	:response Body: Тело ответа содержит информацию о пересылке документа, представленную структурой ``ForwardDocumentResponse``:

		.. code-block:: protobuf

			message ForwardDocumentResponse
			{
			    optional Timestamp ForwardTimestamp = 1;
			    optional ForwardedDocumentId ForwardedDocumentId = 2;
			}

		..

		- ``ForwardTimestamp`` — метка времени пересылки документа, представленная структурой :doc:`../proto/Timestamp`.
		- ``ForwardedDocumentId`` — идентификатор пересланного документа, представленный структурой :doc:`ForwardedDocumentId <../proto/ForwardedDocument>`.

Метод пересылает документ ``ForwardDocumentRequest.DocumentId`` из ящика ``boxId`` третьей стороне в ящик ``ForwardDocumentRequest.ToBoxId``. Адресат пересылки получает снапшот состояния документа на момент времени пересылки.

Допускается пересылка одного документа нескольким получателям и пересылка одного документа несколько раз одному получателю.