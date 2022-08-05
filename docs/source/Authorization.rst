Авторизация
===========

Для авторизации в методы API нужно передавать:
-  Авторизационный токен — массив байтов, однозначно идентифицирующий пользователя.
-  Ключ разработчика — уникальный строковый идентификатор интегратора. Чтобы его получить, оставьте заявку на `странице интеграции <https://www.diadoc.ru/integrations/api>`. Ключ нельзя передавать третьим лицам. 

Эту информацию нужно передать в стандартном HTTP-заголовке :rfc:`Authorization <2617>`.

Схема аутентификации Диадока называется **DiadocAuth**. Для нее определены следующие параметры:

-  ``ddauth_api_client_id`` — определяет ключ разработчика;
-  ``ddauth_token`` — определяет авторизационный токен.


Значения параметров отделяются от их имен символами «=». Параметры разделяются символами «,».

Например:
::

    Authorization: DiadocAuth
    ddauth_api_client_id=testClient-8ee1638deae84c86b8e2069955c2825a,
    ddauth_token=3IU0iPhuhHPZ6lrlumGz4pICEedhQ1XmlMN1Pk8z0DJ51MXkcTi6Q3CODCC4xTMsjPFfhK6XM4kCJ4JJ42hlD499/Ui5WSq6lrPwcdp4IIKswVUwyE0ZiwhlpeOwRjNrvUX1yPrxr0dY8a0w8ePsc1DG8HAlZce8a0hZiWylMqu23d/vfzRFuA==
        

Чтобы получить авторизационный токен по сертификату:
1.	Используйте команду :doc:`http/Authenticate`. В параметре ``ddauth_api_client_id`` HTTP-заголовка ``Authorization`` передайте ключ разработчика.

Пример HTTP-запроса:

::

    POST v3/Authenticate HTTP/1.1
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
        
2.	Расшифруйте тело ответа команды :doc:`http/Authenticate` с помощью закрытого ключа сертификата пользователя. 
3.	Полученный массив байтов закодируйте в :rfc:`Base64 <3548>` - строку.
4.	Передайте результат на вход :doc:`http/AuthenticateConfirm`.

Чтобы получить авторизационный токен по логину и паролю используйте команду :doc:`http/Authenticate`. В параметре ``ddauth_api_client_id`` HTTP-заголовка ``Authorization`` передайте ключ разработчика.
Пример HTTP-запроса:

::

    POST v3/Authenticate?login=user@skbkontur.ru&password=qwerty HTTP/1.1
    Host: diadoc-api.kontur.ru
    Authorization: DiadocAuth ddauth_api_client_id=testClient-8ee1638deae84c86b8e2069955c2825a
    Content-Length: 1252
    Connection: Keep-Alive
        

Успешный ответ сервера:
::

    HTTP/1.1 200 OK
    Content-Length: 598

    <Авторизационный токен>

При вызове методов API к каждому запросу к Диадоку нужно добавлять HTTP-заголовок ``Authorization`` с параметрами ``ddauth_api_client_id`` и ``ddauth_token``.

Например, HTTP-запрос на получение списка доступных пользователю ящиков будет выглядеть так:

::

    POST https://diadoc-api.kontur.ru/GetMyOrganizations HTTP/1.1
    Host: diadoc-api.kontur.ru
    Authorization: DiadocAuth ddauth_api_client_id=testClient-8ee1638deae84c86b8e2069955c2825a,ddauth_token=3IU0iPhuhHPZ6lrlumGz4pICEedhQ1XmlMN1Pk8z0DJ51MXkcTi6Q3CODCC4xTMsjPFfhK6XM4kCJ4JJ42hlD499/Ui5WSq6lrPwcdp4IIKswVUwyE0ZiwhlpeOwRjNrvUX1yPrxr0dY8a0w8ePsc1DG8HAlZce8a0hZiWylMqu23d/vfzRFuA==
        
Методы, работающие с определенным ящиком, контролируют доступ к нему по следующему алгоритму:

1.  Из HTTP-заголовка ``Authorization`` запроса сервер извлекает значение параметра ``ddauth_token``. После декодирования этого значения сервер получает идентификатор пользователя. Если какое-то из вышеперечисленных действий не удалось выполнить, возвращается код ошибки ``401 (Unauthorized) ``. Это возможно в случаях, когда в запросе отсутствует HTTP-заголовок ``Authorization``, нет параметра ``ddauth_token``, токен поврежден или просрочен или указан некорректный ``ddauth_api_client_id``.

2.  По идентификатору пользователя Диадок находит ящики, к которым у пользователя есть доступ. Список ящика совпадает со списком, который вернет метод :doc:`http/GetMyOrganizations`.
3.  Из параметров текущего запроса извлекается идентификатор ящика. Если ящик не из полученного ранее списка, возвращается код ошибки ``403 (Forbidden)``.

Авторизационные токены можно кэшировать. Необязательно вызывать метод :doc:`http/Authenticate` перед каждым обращением к методам API Диадока. Мы рекомендуем использовать токен в течение всего сеанса работы.


----

.. rubric:: Смотри также

*Методы для авторизации:*
- :doc:`http/Authenticate`
- :doc:`http/AuthenticateConfirm`
