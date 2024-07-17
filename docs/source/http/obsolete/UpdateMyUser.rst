UpdateMyUser
============

.. warning::
	Метод устарел и будет удален из API.

Метод ``UpdateMyUser`` изменяет данные текущего авторизованного пользователя, от имени которого делается запрос.

.. http:post:: /UpdateMyUser

	:requestheader Authorization: данные, необходимые для :doc:`авторизации <../../Authorization>`.

	:request Body: Тело запроса должно содержать структуру :doc:`../../proto/obsolete/UserToUpdate`. В структуре нужно значения только те реквизиты пользователя, которые нужно изменить.

	:statuscode 200: операция успешно завершена.
	:statuscode 400: данные в запросе имеют неверный формат или отсутствуют обязательные параметры.
	:statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization`` или в этом заголовке содержатся некорректные авторизационные данные.
	:statuscode 405: используется неподходящий HTTP-метод.
	:statuscode 405: происходит попытка обновить login на уже зарегистрированный на портале.
	:statuscode 500: при обработке запроса возникла непредвиденная ошибка.

	:response Body: Тело ответа содержит измененные данные пользователя, представленные структурой :doc:`../../proto/UserV2`.

Изменение логина пользователя произойдет только после подтверждения нового адреса электронной почты. Пока пользователь не перейдет по ссылке в высланном письме при смене логина, в ответе метода будет указано старое значение логина.

Примеры использования
---------------------

Изменение ФИО и логина пользователя
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

При отправке этого запроса у пользователя будет обновлены ФИО, а на адрес newLogin@kontur.ru будет направлено письмо с ссылкой для подтверждения нового логина.

**Пример HTTP-запроса:**

.. code-block:: http

    POST /UpdateMyUser HTTP/1.1
    Host: diadoc-api.kontur.ru
    Authorization: DiadocAuth ddauth_api_client_id=key, ddauth_token=token
    Content-Type: application/json; charset=utf-8

**Пример тела запроса:**

.. code-block:: json

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

Изменение ФИО
~~~~~~~~~~~~~

При отправке этого запроса у пользователя будет обновлены только ФИО.

**Пример HTTP-запроса:**

.. code-block:: http

    POST /UpdateMyUser HTTP/1.1
    Host: diadoc-api.kontur.ru
    Authorization: DiadocAuth ddauth_api_client_id=key, ddauth_token=token
    Content-Type: application/json; charset=utf-8

**Пример тела запроса:**

.. code-block:: json

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

**Пример тела ответа:**

.. code-block:: http

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