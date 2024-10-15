Authenticate
============

Метод ``Authenticate`` предназначен для аутентификации пользователя в Диадоке.

.. http:post:: /V3/Authenticate

	:queryparam type: способ аутентификации. Параметр не может быть пустым. Может принимать значения:

		- ``password`` — логин и пароль,
		- ``certificate`` — :doc:`сертификат <../entities/certificate>`,
		- ``sid`` — auth.sid.

	:requestheader Authorization: данные, необходимые для авторизации. В заголовке нужно передать ``DiadocAuth ddauth_api_client_id``.

	:request Body: Тело запроса зависит от способа аутентификации.

	:statuscode 200: операция успешно завершена.
	:statuscode 400: данные в запросе имеют неверный формат или отсутствуют обязательные параметры.
	:statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization``, или в этом заголовке отсутствует параметр ``ddauth_api_client_id``, или переданный в нем ключ разработчика не зарегистрирован в Диадоке.
	:statuscode 405: используется неподходящий HTTP-метод.
	:statuscode 500: при обработке запроса возникла непредвиденная ошибка.

	:response Body: Тело ответа зависит от способа аутентификации.

В Диадоке существуют следующие способы аутентификации:

- :ref:`по логину и паролю <auth_login>`,
- :ref:`по сертификату <auth_cert>`,
- :ref:`по auth.sid <auth_sid>`.

.. _auth_login:

Аутентификация по логину и паролю
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Чтобы аутентифицироваться по логину и паролю, укажите в качестве параметра запроса ``type = password``.

В теле запроса передайте сериализованный объект в формате JSON или protobuf:

- Если вы передаете данные в формате JSON, укажите заголовок ``Content-Type: application/json``.


  .. code-block:: json

    {
        "login" : "login",
        "password" : "pass"
    }
  ..

- Если вы передаете данные в формате protobuf, необязательно указывать ``Content-Type``, так как по умолчанию десериализация происходит из protobuf.

  .. code-block:: protobuf

     message LoginPassword {
        required string Login = 1;
        required string Password = 2;
     }

  ..

В теле ответа метод вернет авторизационный токен. 

Пример
""""""

Пример HTTP-запроса:

::

  POST v3/Authenticate?type=password HTTP/1.1
  Host: diadoc-api.kontur.ru
  Authorization: DiadocAuth ddauth_api_client_id=testClient-8ee1638deae84c86b8e2069955c2825a
  Content-Length: 1252
  Connection: Keep-Alive

..

Успешный ответ сервера:

::

  HTTP/1.1 200 OK
  Content-Length: 598

  <Авторизационный токен>

..

.. _auth_cert:

Аутентификация по сертификату
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Чтобы аутентифицироваться по сертификату, укажите в качестве параметра запроса ``type = certificate``.

Укажите заголовок ``Content-Type: application/octet-stream``, в теле запроса передайте бинарное содержимое открытого ключа сертификата.

В теле ответа метод вернет зашифрованную строку. Чтобы получить из нее авторизационный токен:

#. Расшифруйте тело ответа с помощью закрытого ключа сертификата пользователя, используя для этого сервис криптопровайдера. Для упрощения работы с API используйте :ref:`SDK <integration>`: он содержит реализацию механизма аутентификации по сертификату.
#. Полученный после расшифровки массив байтов закодируйте в :rfc:`Base64 <3548>`-строку.
#. Передайте закодированную строку в метод :doc:`AuthenticateConfirm`, он вернет авторизационный токен.

Пример
""""""

Пример HTTP-запроса:

::

  POST v3/Authenticate?type=certificate HTTP/1.1
  Host: diadoc-api.kontur.ru
  Authorization: DiadocAuth ddauth_api_client_id=testClient-8ee1638deae84c86b8e2069955c2825a
  Content-Length: 1252
  Connection: Keep-Alive

  <Двоичное DER-представление X.509-сертификата пользователя>

..

Успешный ответ сервера:

::

  HTTP/1.1 200 OK
  Content-Length: 598

  <Двоичное DER-представление зашифрованного токена>

..

.. _auth_sid:

Аутентификация по auth.sid
~~~~~~~~~~~~~~~~~~~~~~~~~~

Если вы получили идентификатор auth.sid из других сервисов, вы можете использовать его для аутентификации в Диадоке.

Чтобы аутентифицироваться по auth.sid, укажите в качестве параметра запроса ``type = sid``.
В теле запроса нужно передавать ``auth.sid`` c заголовком ``Content-Type: text/plain``


SDK
---

Пример кода на C# для получения авторизационного токена:

.. code-block:: csharp

    //URL веб-сервиса Диадок
    private const string DefaultApiUrl = "https://diadoc-api.kontur.ru";

    //Идентификатор клиента
    private const string DefaultClientId = "test-8ee1638deae84c86b8e2069955c2825a";

    //Для использования Диадок требуются:
    //1. Крипто-API, предоставляемое операционной системой (доступно через класс WinApiCrypt)
    //2. Экземпляр класса DiadocApi, проксирующий работу с веб-сервисом Диадок
    private static WinApiCrypt Crypt = new WinApiCrypt();
    public static readonly DiadocApi Api = new DiadocApi(
        DefaultClientId,
        DefaultApiUrl,
        Crypt);

    //Логин для авторизации на сервере Диадок

    private const string DefaultLogin = "логин";

    //Пароль для авторизации на сервере Диадок
    private const string DefaultPassword = "пароль";

    //Путь к сертификату для авторизации на сервере Диадок
    public const string DefaultPathToCert = "C:\\folder\\subfolder\\cert.cer";

    //Для авторизации по сертификату необходимо сертификат преобразовать в массив байтов
    public static byte[] ReadCertContent(string pathToCert)
    {
        var cert = new X509Certificate(pathToCert); 
        return cert.Export(X509ContentType.Cert);
    }

    static void Main(string[] args)
    {
        //Можно использовать либо аутентификацию по логину/паролю, либо по сертификату
        var authTokenLogin = Api.Authenticate(DefaultLogin, DefaultPassword); //по паре логин/пароль
        var authTokenCert = Api.Authenticate(ReadCertContent(DefaultPathToCert)); //по сертификату
    }

----

.. rubric:: См. также

*Инструкции:*
	- :doc:`Авторизация <../Authorization>`

*Другие методы для аутентификации:*
	- :doc:`AuthenticateConfirm` — возвращает авторизационный токен при аутентификации по сертификату