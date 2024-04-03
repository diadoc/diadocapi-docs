DssSignResult
=============

Метод ``DssSignResult`` возвращает результат операции подписания файлов сертификатом без носителя, выполняемой методом :doc:`DssSign`.

.. http:get:: /DssSignResult

	:queryparam boxId: идентификатор :doc:`ящика <../entities/box>` организации.
	:queryparam taskId: идентификатор операции, полученный методом :doc:`DssSign`.

	:requestheader Authorization: данные, необходимые для :doc:`авторизации <../Authorization>`.

	:statuscode 200: операция успешно завершена.
	:statuscode 400: данные в запросе имеют неверный формат или отсутствуют обязательные параметры.
	:statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization`` или в этом заголовке содержатся некорректные авторизационные данные.
	:statuscode 402: у организации с указанным ``boxId`` закончилась подписка на API.
	:statuscode 403: доступ к ящику с предоставленным авторизационным токеном запрещен.
	:statuscode 404: не найден ящик или операция с указанными идентификаторами.
	:statuscode 405: используется неподходящий HTTP-метод.
	:statuscode 500: при обработке запроса возникла непредвиденная ошибка.

	:response Body: Тело ответа содержит результат операции подписания файлов, представленный структурой :doc:`../proto/DssSignResult`.

Примеры ответов
---------------

::

    HTTP/1.1 200 OK
    Content-Type: application/json; charset=utf-8

    {
        "OperationStatus": "InProgress",
        "DssFileSigningResult": []
    }

::

    HTTP/1.1 200 OK
    Content-Type: application/json; charset=utf-8

    {
        "OperationStatus": "Completed",
        "DssFileSigningResult": [
            {
                "FileSigningStatus": "SigningCompleted",
                "Signature": "<signatureBytesBase64>"
            },
            {
                "FileSigningStatus": "SigningCompleted",
                "Signature": "<signatureBytesBase64>"
            },
            {
                "FileSigningStatus": "SigningCompleted",
                "Signature": "<signatureBytesBase64>"
            }
        ]
    }
