GetEmployee
===========

.. http:get:: /GetEmployee

    :query boxId: идентификатор ящика
    :query userId: идентификатор пользователя

    :reqheader Authorization: необходимые данные для :doc:`авторизации <../Authorization>`

    :statuscode 200: операция успешно завершена
    :statuscode 400: данные в запросе имеют неверный формат или отсутствуют обязательные параметры
    :statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization``, или в этом заголовке содержатся некорректные авторизационные данные
    :statuscode 402: закончилась подписка на API
    :statuscode 403: доступ к ящику с предоставленным авторизационным токеном запрещен или запрос сделан не от имени администратора
    :statuscode 404: в указанном ящике нет пользователя с указанным идентификатором
    :statuscode 405: используется неподходящий HTTP-метод
    :statuscode 500: при обработке запроса возникла непредвиденная ошибка

**Тело ответа:** :doc:`../proto/Employee`

Возвращает информацию о сотруднике организации. Запрос доступен только администраторам организации.

Пример ответа
-------------

::

    HTTP/1.1 200 OK
    Content-Type: application/json; charset=utf-8

    {
        "User": {
            "UserId": "fccbb0a6-0700-4401-81a6-8a6a083e12e6",
            "Login": "email@example.com",
            "FullName": {
                "LastName": "Иванов",
                "FirstName": "Иван",
                "MiddleName": "Иванович"
            },
            "IsRegistered": true
        },
        "Permissions": {
            "UserDepartmentId": "00000000-0000-0000-0000-000000000000",
            "IsAdministrator": false,
            "DocumentAccessLevel": "AllDocuments",
            "Actions": [
                { "Name": "CreateDocuments", "IsAllowed": true },
                { "Name": "DeleteRestoreDocuments", "IsAllowed": true },
                { "Name": "SignDocuments", "IsAllowed": true },
                { "Name": "AddResolutions", "IsAllowed": false },
                { "Name": "RequestResolutions", "IsAllowed": false },
                { "Name": "ManageCounteragents", "IsAllowed": true }
            ]
        },
        "Position": "Бухгалтер",
        "CanBeInvitedForChat": true,
        "CreationTimestamp": {
            "DateTime": "2018-11-01T05:40:17.6953926Z",
            "Ticks": 636766476176953926
        }
    }
