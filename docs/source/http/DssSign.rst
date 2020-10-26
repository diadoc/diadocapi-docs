DssSign
=======

.. http:post:: /DssSign

    :query boxId: идентификатор ящика
    :query certificateThumbprint: отпечаток сертификата без носителя, которым требуется подписать файлы. Если не передан, будет использован неистекший сертификат без носителя с самым длительным сроком действия, привязанный к пользователю в Диадоке

    :reqheader Authorization: необходимые данные для :doc:`авторизации <../Authorization>`

    :statuscode 200: операция успешно завершена
    :statuscode 400: данные в запросе имеют неверный формат или отсутствуют обязательные параметры
    :statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization``, или в этом заголовке содержатся некорректные авторизационные данные
    :statuscode 402: закончилась подписка на API
    :statuscode 403: доступ к ящику с предоставленным авторизационным токеном запрещен
    :statuscode 404: не найден ящик с таким идентификатором или DSS-сертификат
    :statuscode 405: используется неподходящий HTTP-метод
    :statuscode 500: при обработке запроса возникла непредвиденная ошибка

**Тело запроса:** :doc:`../proto/DssSignRequest`

**Тело ответа:** :doc:`../proto/AsyncMethodResult`

Метод запускает асинхронную операцию подписания нескольких файлов сертификатом без носителя.

Метод возвращает идентификатор операции подписания. Чтобы получить результат подписания, необходимо передать этот идентификатор в метод :doc:`DssSignResult`.

Пример запроса
--------------

.. sourcecode:: http

    POST /DssSign?boxId=54e9ca30-09c3-4bc9-926f-8f3c1ab56ca3&certificateThumbprint=8A80C2723DBC4F0A94F8CEE21C0A15A68A80C272 HTTP/1.1
    Host: diadoc-api.kontur.ru
    Authorization: DiadocAuth ddauth_api_client_id=key, ddauth_token=token
    Content-Type: application/json; charset=utf-8
    
    {
        "Files": [
            {
                "Content": {
                    "Content": "<fileBytesBase64>"
                },
                "FileName": "first.xml"
            },
            {
                "Content": {
                    "NameOnShelf": "__userId__/478DCC82-6CD1-4A26-B8F7-7E3E52DC5C81"
                },
                "FileName": "second.xml"
            },
            {
                "Content": {
                    "EntityId": {
                        "MessageId": "ab149008-561e-42aa-a639-8873a64ceaaf",
                        "EntityId": "f92492f0-f5fc-4de6-898c-6b77c83d0dba"
                    }
                },
                "FileName": "third.xml"
            },
            {
                "Content": {
                    "PatchedContentId": "0AD643FD-C76F-4408-B6B8-1964F9A40AD5"
                },
                "FileName": "fourth.xml"
            }
        ]
    }

Пример ответа
-------------

::

    HTTP/1.1 200 OK
    Content-Type: application/json; charset=utf-8

    {
        "TaskId": "2fd45887-138e-4e08-aeb2-bcd55bf0dd85"
    }
