Авторизация
===========

Дяя работы с API нужна авторизация. Для авторизации в методы API нужно передавать:

- авторизационный токен — массив байтов, однозначно идентифицирующий пользователя;
- ключ разработчика — уникальный строковый идентификатор интегратора. Чтобы получить ключ разработчика, оставьте заявку на `странице интеграции <https://www.diadoc.ru/integrations/api>`__. Не передавайте ключ третьим лицам. 

Эту информацию нужно передавать в стандартном HTTP-заголовке ``Authorization``.

Схема аутентификации Диадока называется **DiadocAuth**. Для нее определены следующие параметры:

- ``ddauth_api_client_id`` — определяет ключ разработчика,
- ``ddauth_token`` — определяет авторизационный токен.


Значения параметров в заголовке отделяются от их имен символами «=». Параметры разделяются символами «,».

Например:
::

    Authorization: DiadocAuth
    ddauth_api_client_id=testClient-8ee1638deae84c86b8e2069955c2825a,
    ddauth_token=3IU0iPhuhHPZ6lrlumGz4pICEedhQ1XmlMN1Pk8z0DJ51MXkcTi6Q3CODCC4xTMsjPFfhK6XM4kCJ4JJ42hlD499/Ui5WSq6lrPwcdp4IIKswVUwyE0ZiwhlpeOwRjNrvUX1yPrxr0dY8a0w8ePsc1DG8HAlZce8a0hZiWylMqu23d/vfzRFuA==
        

Есть четыре способа получения авторизационного токена:
- по сертификату,
- по логину и паролю,
- по auth.sid,
- доверительная авторизация.

Чтобы получить авторизационный токен по сертификату:

#. Используйте команду :doc:`http/Authenticate`. 
#. В параметре ``ddauth_api_client_id`` HTTP-заголовка ``Authorization`` передайте ключ разработчика.

Пример HTTP-запроса:

::

    POST v3/Authenticate?type=certificate HTTP/1.1
    Host: diadoc-api.kontur.ru
    Authorization: DiadocAuth ddauth_api_client_id=testClient-8ee1638deae84c86b8e2069955c2825a
    Content-Length: 1252
    Connection: Keep-Alive

    <Двоичное DER-представление X.509-сертификата пользователя> 

Успешный ответ сервера:
::

    HTTP/1.1 200 OK
    Content-Length: 598

    <Двоичное DER-представление зашифрованного токена>
        
#.	Расшифруйте тело ответа команды :doc:`http/Authenticate` с помощью закрытого ключа сертификата пользователя. 
#.	Полученный после расшифровки массив байтов закодируйте в :rfc:`Base64 <3548>`-строку.
#.	Чтобы получить авторизационный токен, передайте результат на вход :doc:`http/AuthenticateConfirm`.

Чтобы получить авторизационный токен по логину и паролю:
#. Используйте метод :doc:`http/Authenticate`. 
#. В параметре ``ddauth_api_client_id`` HTTP-заголовка ``Authorization`` передайте ключ разработчика.
#. Метод вернет авторизационный токен.

Пример HTTP-запроса:

::

    POST v3/Authenticate?type=password HTTP/1.1
    Host: diadoc-api.kontur.ru
    Authorization: DiadocAuth ddauth_api_client_id=testClient-8ee1638deae84c86b8e2069955c2825a
    Content-Length: 1252
    Connection: Keep-Alive
        

Успешный ответ сервера:
::

    HTTP/1.1 200 OK
    Content-Length: 598

    <Авторизационный токен>

Для авторизации при вызове методов API к каждому запросу к Диадоку нужно добавлять HTTP-заголовок ``Authorization`` с параметрами ``ddauth_api_client_id`` и ``ddauth_token``. Например, HTTP-запрос на получение списка доступных пользователю ящиков будет выглядеть так:

::

    POST https://diadoc-api.kontur.ru/GetMyOrganizations HTTP/1.1
    Host: diadoc-api.kontur.ru
    Authorization: DiadocAuth ddauth_api_client_id=testClient-8ee1638deae84c86b8e2069955c2825a,ddauth_token=3IU0iPhuhHPZ6lrlumGz4pICEedhQ1XmlMN1Pk8z0DJ51MXkcTi6Q3CODCC4xTMsjPFfhK6XM4kCJ4JJ42hlD499/Ui5WSq6lrPwcdp4IIKswVUwyE0ZiwhlpeOwRjNrvUX1yPrxr0dY8a0w8ePsc1DG8HAlZce8a0hZiWylMqu23d/vfzRFuA==
        
Методы, работающие с определенным ящиком, контролируют доступ к нему по следующему алгоритму:

1.  Сервер Диадока извлекает из HTTP-заголовка ``Authorization`` значение параметра ``ddauth_token``. После его декодирования сервер получает идентификатор пользователя. Если какое-то из вышеперечисленных действий не удалось выполнить, возвращается код ошибки ``401 (Unauthorized) ``. Это возможно в случаях, когда в запросе отсутствует HTTP-заголовок ``Authorization``, нет параметра ``ddauth_token``, токен поврежден или просрочен или указан некорректный ``ddauth_api_client_id``.
2.  По идентификатору пользователя Диадок находит ящики, к которым у пользователя есть доступ. Список ящиков совпадает со списком, который вернет метод :doc:`http/GetMyOrganizations`.
3.  Сервер извлекает идентификатор ящика из параметров запроса. Если у пользователя нет доступа к ящику, метод вернет код ошибки ``403 (Forbidden)``.

Авторизационные токены можно кэшировать: необязательно вызывать метод :doc:`http/Authenticate` перед каждым обращением к методам API Диадока. Мы рекомендуем сохранить и использовать полученный токен в течение всего сеанса работы.


----

.. rubric:: Смотри также

*Методы для авторизации:*

- :doc:`http/Authenticate`
- :doc:`http/AuthenticateConfirm`
