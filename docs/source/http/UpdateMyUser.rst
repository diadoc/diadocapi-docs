UpdateMyUser
============

.. http:post:: /UpdateMyUser

    :reqheader Authorization: необходимые данные для :doc:`авторизации <../Authorization>`

    :statuscode 200: операция успешно завершена
    :statuscode 400: данные в запросе имеют неверный формат или отсутствуют обязательные параметры
    :statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization``, или в этом заголовке содержатся некорректные авторизационные данные
    :statuscode 405: используется неподходящий HTTP-метод
    :statuscode 405: происходит попытка обновить login на уже зарегистрированный на портале
    :statuscode 500: при обработке запроса возникла непредвиденная ошибка

**Тело запроса:** :doc:`../proto/UserToUpdate`

**Тело ответа:** :doc:`../proto/UserV2`

Позволяет изменить данные текущего авторизованного пользователя, от имени которого делается запрос. В запросе достаточно передать значения только тех реквизитов пользователя, которые необходимо изменить.

Метод возвращает пользователя после изменения (*Изменение логина пользователя произойдет только после подтверждения нового адреса электронной почты*).

Примеры использования
---------------------

**Пример запроса**:

.. sourcecode:: http

    POST /UpdateMyUser HTTP/1.1
    Host: diadoc-api.kontur.ru
    Authorization: DiadocAuth ddauth_api_client_id=key, ddauth_token=token
    Content-Type: application/json; charset=utf-8

    {
        "Login":
        {
            "Login": "newLogin@kontur.ru"
        },
        "FullName":
        {
            "FullName":
            {
                "FirstName": "NewFirstName",
                "LastName": "NewLastName",
                "MiddleName": "NewMiddleName"
            }
        }
    }

Запрос приведет к тому, что у пользователя будет обновлено ФИО, а также на адрес newLogin@kontur.ru будет направлено письмо с ссылкой для подтверждения нового логина.

**Пример запроса для обновления ФИО**:

.. sourcecode:: http

    POST /UpdateMyUser HTTP/1.1
    Host: diadoc-api.kontur.ru
    Authorization: DiadocAuth ddauth_api_client_id=key, ddauth_token=token
    Content-Type: application/json; charset=utf-8

    {
        "FullName":
        {
            "FullName":
            {
                "FirstName": "NewFirstName",
                "LastName": "NewLastName",
                "MiddleName": "NewMiddleName"
            }
        }
    }

Запрос приведет к тому, что у пользователя будет обновлено только ФИО.

**Пример запроса с использованием C# SDK**:

.. code-block:: csharp

        api.UpdateMyUser(token, new UserToUpdate
            {
                Login = new UserLoginPatch
                {
                    Login = "newLogin@kontur.ru"
                },
                FullName = new UserFullNamePatch
                {
                    FullName = new FullName
                    {
                        FirstName = "NewFirstName",
                        LastName = "NewLastName",
                        MiddleName = "NewMiddleName"
                    }
                }
            });

**Пример ответа**:

::

    HTTP/1.1 200 OK
    Content-Type: application/json; charset=utf-8

    {
        "UserId": "d064f6ba-7b81-432d-a41d-93b23eebe579",
        "Login": "login@kontur.ru",
        "FullName":
        {
            "FirstName": "NewFirstName",
            "LastName": "NewLastName",
            "MiddleName": "NewMiddleName"
        },
        "IsRegistered": true
    }

До тех пор, пока пользователь не перейдет по ссылке в высланном при смене логина письме, в ответе будет указано старое значение логина.