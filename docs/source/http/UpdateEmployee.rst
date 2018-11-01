UpdateEmployee
==============

.. http:post:: /UpdateEmployee

    :query boxId: идентификатор ящика
    :query userId: идентификатор пользователя

    :reqheader Authorization: необходимые данные для :doc:`авторизации <../Authorization>`

    :statuscode 200: операция успешно завершена
    :statuscode 400: данные в запросе имеют неверный формат или отсутствуют обязательные параметры
    :statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization``, или в этом заголовке содержатся некорректные авторизационные данные
    :statuscode 402: закончилась подписка на API
    :statuscode 403: доступ к ящику с предоставленным авторизационным токеном запрещен или запрос сделан не от имени администратора
    :statuscode 405: используется неподходящий HTTP-метод
    :statuscode 500: при обработке запроса возникла непредвиденная ошибка

**Тело запроса:** :doc:`../proto/EmployeeToUpdate`

**Тело ответа:** :doc:`../proto/Employee`

Изменяет данные сотрудника организации.

В ответе будет информация о сотруднике после изменения.

Запрос доступен только администраторам организации.

Примеры использования
---------------------

Пример 1
~~~~~~~~

Изменение уровня доступа к документам, списка доступных подразделений и должности

Пример запроса
^^^^^^^^^^^^^^

.. sourcecode:: http

    POST /UpdateEmployee?boxId=994cf191-8322-40eb-8d79-f1196f8ec357&userId=fccbb0a6-0700-4401-81a6-8a6a083e12e6 HTTP/1.1
    Host: diadoc-api.kontur.ru
    Authorization: DiadocAuth ddauth_api_client_id=key, ddauth_token=token
    Content-Type: application/json; charset=utf-8

    {
        "Permissions": {
            "DocumentAccessLevel": {
                "DocumentAccessLevel": "SelectedDepartments"
            },
            "SelectedDepartments": {
                "SelectedDepartmentIds": [
                    "7e49e042-8a0f-478d-a4e0-5e9273c47b20",
                    "2f2f67bc-b5fe-4662-9e4f-b09348b44582"
                ]
            },
        },
        "Position": {
            "Position": "Бухгалтер"
        }
    }

С использованием C# SDK
^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: csharp

    var employee = api.UpdateEmployee(
        token,
        boxId,
        userId,
        new EmployeeToUpdate
        {
            Permissions = new EmployeePermissionsPatch
            {
                DocumentAccessLevel = new EmployeeDocumentAccessLevelPatch
                {
                    DocumentAccessLevel = DocumentAccessLevel.SelectedDepartments
                },
                SelectedDepartments = new EmployeeSelectedDepartmentsPatch
                {
                    SelectedDepartmentIds =
                    {
                        "7e49e042-8a0f-478d-a4e0-5e9273c47b20",
                        "2f2f67bc-b5fe-4662-9e4f-b09348b44582"
                    }
                }
            },
            Position = new EmployeePositionPatch
            {
                Position = "Бухгалтер"
            }
        });

Пример 2
~~~~~~~~

Изменение подразделения, права администрировать организацию, доступных действий и необходимости показывать в списке получателей Сообщений

Пример запроса
^^^^^^^^^^^^^^

.. sourcecode:: http

    POST /UpdateEmployee?boxId=994cf191-8322-40eb-8d79-f1196f8ec357&userId=fccbb0a6-0700-4401-81a6-8a6a083e12e6 HTTP/1.1
    Host: diadoc-api.kontur.ru
    Authorization: DiadocAuth ddauth_api_client_id=key, ddauth_token=token
    Content-Type: application/json; charset=utf-8

    {
        "Permissions": {
            "Department": {
                "DepartmentId": "11c8276b-815f-4191-adea-c0f884429624"
            },
            "IsAdministrator": {
                "IsAdministrator": true
            },
            "Actions": [
                { "Name": "ManageCounteragents", "IsAllowed": true },
                { "Name": "SignDocuments", "IsAllowed": false }
            ]
        },
        "CanBeInvitedForChat": {
            "CanBeInvitedForChat": true
        }
    }

С использованием C# SDK
^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: csharp

    var employee = api.UpdateEmployee(
        token,
        boxId,
        userId,
        new EmployeeToUpdate
        {
            Permissions = new EmployeePermissionsPatch
            {
                Department = new EmployeeDepartmentPatch
                {
                    DepartmentId = "11c8276b-815f-4191-adea-c0f884429624"
                },
                IsAdministrator = new EmployeeIsAdministratorPatch
                {
                    IsAdministrator = true
                },
                Actions =
                {
                    new EmployeeAction
                    {
                        Name = "ManageCounteragents",
                        IsAllowed = true
                    },
                    new EmployeeAction
                    {
                        Name = "SignDocuments",
                        IsAllowed = false
                    }
                }
            },
            CanBeInvitedForChat = new EmployeeCanBeInvitedForChatPatch
            {
                CanBeInvitedForChat = true
            }
        });
