GetEmployees
============

.. http:get:: /GetEmployees

    :query boxId: идентификатор ящика
    :query page: номер страницы, начиная с 1, необязательный, по умолчанию 1
    :query count: количество сотрудников на странице, от 1 до 50, необязательный, по умолчанию 50

    :reqheader Authorization: необходимые данные для :doc:`авторизации <../Authorization>`

    :statuscode 200: операция успешно завершена
    :statuscode 400: данные в запросе имеют неверный формат или отсутствуют обязательные параметры
    :statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization``, или в этом заголовке содержатся некорректные авторизационные данные
    :statuscode 402: закончилась подписка на API
    :statuscode 403: доступ к ящику с предоставленным авторизационным токеном запрещен или запрос сделан не от имени администратора
    :statuscode 404: указанного ящика не существует
    :statuscode 405: используется неподходящий HTTP-метод
    :statuscode 500: при обработке запроса возникла непредвиденная ошибка

**Тело ответа:** :doc:`../proto/EmployeeList`

Возвращает список сотрудников организации.

Сотрудники сортируются по признаку *IsRegistered* струкуры :doc:`../proto/UserV2` (сначала выводятся сотрудники без учетной записи в системе), а затем по дате создания в прямом порядке.

Сотрудники возвращаются постранично, для навигации используется параметр *page*.

Запрос доступен только администраторам организации.

Примеры использования
---------------------

Пример запроса
~~~~~~~~~~~~~~

.. sourcecode:: http

    GET /GetEmployees?boxId=994cf191-8322-40eb-8d79-f1196f8ec357&page=2&count=10 HTTP/1.1
    Host: diadoc-api.kontur.ru
    Authorization: DiadocAuth ddauth_api_client_id=key, ddauth_token=token
    Accept: application/json

Пример ответа
~~~~~~~~~~~~~

::

    HTTP/1.1 200 OK
    Content-Type: application/json; charset=utf-8

    {
        "Employees": [{
            "User": {
                "UserId": "5c573ff4-d336-4956-8261-26d0576c4718",
                "Login": "ivan@example.com",
                "FullName": {
                    "LastName": "Иванов",
                    "FirstName": "Иван",
                    "MiddleName": "Иванович"
                },
                "IsRegistered": false
            },
            "Position": "Бухгалтер",
            /* ... */
        }, {
            "User": {
                "UserId": "abc8398b-71c2-4efd-9339-003af3758a58",
                "Login": "petr@example.com",
                "FullName": {
                    "LastName": "Петров",
                    "FirstName": "Петр",
                    "MiddleName": "Петрович"
                },
                "IsRegistered": true
            },
            "Position": "Директор",
            /* ... */
        }
        /* ... */
        ],
        "TotalCount": 61
    }


Пример загрузки полного списка сотрудников (C#)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: csharp

    var employees = new List<Employee>();

    for (var page = 1;; page++)
    {
        var employeeList = api.GetEmployees(token, boxId, page, count: 10);
        employees.AddRange(employeeList.Employees);

        Console.WriteLine("{0}/{1}", employees.Count, employeeList.TotalCount);

        if (employeeList.Employees.Count == 0 || employees.Count >= employeeList.TotalCount)
        {
            break;
        }
    }
