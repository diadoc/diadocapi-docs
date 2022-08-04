Авторизация
===========

Для авторизации во все методы интеграторского интерфейса нужно передавать авторизационный токен — массив байтов, однозначно идентифицирующий пользователя, и ключ разработчика — уникальный строковый идентификатор интегратора.  
Оставьте заявку по адресу https://www.diadoc.ru/integrations/api, чтобы получить ключ. Ключ разработчика нельзя передавать третьим лицам.


Для передачи авторизационной информации используется стандартный HTTP-заголовок :rfc:`Authorization <2617>`.

Схема аутентификации Диадока называется **DiadocAuth**. Для нее определены следующие параметры:

-  ``ddauth_api_client_id`` — служит для передачи ключа разработчика;
-  ``ddauth_token`` — служит для передачи авторизационного токена.

.. note:: Значения параметров отделяются от их имен символами «=». Параметры разделяются символами «,».

Например:
::

    Authorization: DiadocAuth
    ddauth_api_client_id=testClient-8ee1638deae84c86b8e2069955c2825a,
    ddauth_token=3IU0iPhuhHPZ6lrlumGz4pICEedhQ1XmlMN1Pk8z0DJ51MXkcTi6Q3CODCC4xTMsjPFfhK6XM4kCJ4JJ42hlD499/Ui5WSq6lrPwcdp4IIKswVUwyE0ZiwhlpeOwRjNrvUX1yPrxr0dY8a0w8ePsc1DG8HAlZce8a0hZiWylMqu23d/vfzRFuA==
        

Для получения авторизационного токена используйте команду :doc:`http/Authenticate`.

В параметре ``ddauth_api_client_id`` HTTP-заголовка ``Authorization`` нужно передать ключ разработчика.

HTTP-запрос выглядит следующим образом::

::

    POST https://diadoc-api.kontur.ru/v3/Authenticate HTTP/1.1
    Host: diadoc-api.kontur.ru
    Authorization: DiadocAuth ddauth_api_client_id=testClient-8ee1638deae84c86b8e2069955c2825a
    Content-Length: 1252
    Connection: Keep-Alive

    <Двоичное DER-представление X.509-сертификата пользователя>
        

Успешный ответ сервера выглядит так:
::

    HTTP/1.1 200 OK
    Content-Length: 598

    <Двоичное DER-представление зашифрованного токена>
        
Расшифруйте тело ответа команды :doc:`http/Authenticate` с помощью закрытого ключа сертификата пользователя. Полученный массив байтов закодируйте в :rfc:`Base64 <3548>` - строку и передайте результат на вход :doc:`http/AuthenticateConfirm` 

После к каждому HTTP-запросу к Диадоку нужно добавлять HTTP-заголовок ``Authorization`` с параметрами ``ddauth_api_client_id`` и ``ddauth_token``.

Например, команда получения списка доступных пользователю ящиков транслируется в следующий HTTP-запрос:
::

    POST https://diadoc-api.kontur.ru/GetMyOrganizations HTTP/1.1
    Host: diadoc-api.kontur.ru
    Authorization: DiadocAuth ddauth_api_client_id=testClient-8ee1638deae84c86b8e2069955c2825a,ddauth_token=3IU0iPhuhHPZ6lrlumGz4pICEedhQ1XmlMN1Pk8z0DJ51MXkcTi6Q3CODCC4xTMsjPFfhK6XM4kCJ4JJ42hlD499/Ui5WSq6lrPwcdp4IIKswVUwyE0ZiwhlpeOwRjNrvUX1yPrxr0dY8a0w8ePsc1DG8HAlZce8a0hZiWylMqu23d/vfzRFuA==
        
Для команд, предусматривающих работу с определенным ящиком, контроль доступа к ящику работает по следующему алгоритму:

1.  Из HTTP-заголовка Authorization текущего запроса извлекается значение параметра ``ddauth_token``. Это значение декодируется и из него извлекается идентификатор пользователя.

  1. Если в запросе отсутствует HTTP-заголовок ``Authorization``, нет параметра ``ddauth_token``, токен поврежден или просрочен или указан некорректный ``ddauth_api_client_id``, то возвращается код ошибки ``401 (Unauthorized) ``.

2.  По идентификатору пользователя находится множество ящиков, к которым у пользователя есть доступ. Это же множество возвращает метод :doc:`http/GetMyOrganizations`.
3.  Из параметров текущего запроса извлекается идентификатор ящика. Если идентификатор ящика не принадлежит множеству, полученному на предыдущем шаге, то возвращается код ошибки ``403 (Forbidden)``.
4.  Иначе доступ разрешается.

Авторизационные токены можно на некоторое время кэшировать. Вызывать метод :doc:`http/Authenticate` перед каждым обращением к методам API Диадока необязательно. Рекомендуемая стратегия заключается в получении токена на сеанс работы и его использовании в течение этого сеанса.

HTTP-интерфейс
--------------

.. toctree::
   :name: toc1
   :maxdepth: 1
   
   http/Authenticate
   http/AuthenticateConfirm
