DssSignResult
=============

.. http:get:: /DssSignResult

    :query boxId: идентификатор ящика
    :query taskId: идентификатор операции, полученный методом :doc:`DssSign`

    :reqheader Authorization: необходимые данные для :doc:`авторизации <../Authorization>`

    :statuscode 200: запрос выполнен успешно
    :statuscode 400: данные в запросе имеют неверный формат или отсутствуют обязательные параметры
    :statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization``, или в этом заголовке содержатся некорректные авторизационные данные
    :statuscode 402: закончилась подписка на API
    :statuscode 403: доступ к ящику с предоставленным авторизационным токеном запрещен
    :statuscode 404: не найден ящик или операция с таким идентификатором
    :statuscode 405: используется неподходящий HTTP-метод
    :statuscode 500: при обработке запроса возникла непредвиденная ошибка

**Тело ответа:** :doc:`../proto/DssSignResult`

Метод возвращает результат операции подписания файлов DSS-сертификатом.

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
