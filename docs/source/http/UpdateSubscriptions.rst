UpdateSubscriptions
===================

.. http:post:: /UpdateSubscriptions

    :query boxId: идентификатор ящика
    :query userId: идентификатор пользователя

    :reqheader Authorization: необходимые данные для :doc:`авторизации <../Authorization>`

    :statuscode 200: операция успешно завершена
    :statuscode 400: данные в запросе имеют неверный формат или отсутствуют обязательные параметры
    :statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization``, или в этом заголовке содержатся некорректные авторизационные данные
    :statuscode 402: закончилась подписка на API
    :statuscode 403: доступ к ящику с предоставленным авторизационным токеном запрещен или запрос сделан не от имени администратора и не от имени пользователя, подписки которого редактируются
    :statuscode 404: в указанном ящике нет пользователя с указанным идентификатором
    :statuscode 405: используется неподходящий HTTP-метод
    :statuscode 500: при обработке запроса возникла непредвиденная ошибка

**Тело запроса:** :doc:`../proto/SubscriptionsToUpdate`

**Тело ответа:** :doc:`../proto/EmployeeSubscriptions`

Изменяет статус подписок сотрудника организации на конкретные почтовые уведомления. В запросе достаточно передать значения только для тех уведомлений, на которые требуется подписать пользователя и от которых необходимо отписать.

Метод возвращает подписки сотрудника после изменения.

Запрос доступен только администраторам организации и пользователю, подписки которого редактируются.

Примеры использования
---------------------

**Пример запроса**:

.. sourcecode:: http

    POST /UpdateSubscriptions?boxId=994cf191-8322-40eb-8d79-f1196f8ec357&userId=fccbb0a6-0700-4401-81a6-8a6a083e12e6 HTTP/1.1
    Host: diadoc-api.kontur.ru
    Authorization: DiadocAuth ddauth_api_client_id=key, ddauth_token=token
    Content-Type: application/json; charset=utf-8

    {
        "Subscriptions": [
            { "Id": "NewIncomingDocuments", "IsSubscribed": "true" },
            { "Id": "News", "IsSubscribed": "false" }
        ]
    }

Запрос приведет к тому, что пользователь подпишется на уведомления о новых входящих документах и отпишется от новостей Диадока.

**Пример запроса с использованием C# SDK**:

.. code-block:: csharp

    api.UpdateSubscriptions(token, boxId, userId, new SubscriptionsToUpdate
        {
            Subscriptions =
            {
                new Subscription { Id = "NewIncomingDocuments", IsSubscribed = true },
                new Subscription { Id = "News", IsSubscribed = false },
            }
        });

**Пример ответа**:

::

    HTTP/1.1 200 OK
    Content-Type: application/json; charset=utf-8

    {
        "Subscriptions": [
            { "Id": "CounteragentInvitation", "IsSubscribed": "false" },
            ...
            { "Id": "NewIncomingDocuments", "IsSubscribed": "true" },
            { "Id": "News", "IsSubscribed": "false" },
            ...
            { "Id": "ChatMessages", "IsSubscribed": "true" }
        ]
    }

В ответе будет состояние всех подписок сотрудника на почтовые уведомления.