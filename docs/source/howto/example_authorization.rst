Как авторизоваться в системе
============================

Большинству команд интеграторского интерфейса требуется авторизация. Для этого команды требуют в качестве обязательного параметра авторизационный токен — массив байтов, однозначно идентифицирующий пользователя.

Кроме того, во все методы интеграторского интерфейса требуется передавать "ключ разработчика" — уникальный строковый идентификатор интегратора, который можно получить, написав запрос по адресу diadoc-api@skbkontur.ru. Интегратор не должен передавать свой "ключ разработчика" третьим лицам.

Для передачи авторизационной информации с каждым запросом используется стандартный HTTP-заголовок :rfc:`Authorization <2617>`.

Схема аутентификации, используемая Диадоком, называется **DiadocAuth**. Для нее определены следующие параметры:

-  *ddauth_api_client_id* — ключ разработчика;
-  *ddauth_token* — авторизационный токен.

.. note:: Значения параметров отделяются от их имен символами '='. Параметры разделяются символами ',' .

Например:
::

    Authorization: DiadocAuth
    ddauth_api_client_id=testClient-8ee1638deae84c86b8e2069955c2825a,
    ddauth_token=3IU0iPhuhHPZ6lrlumGz4pICEedhQ1XmlMN1Pk8z0DJ51MXkcTi6Q3CODCC4xTMsjPFfhK6XM4kCJ4JJ42hlD499/Ui5WSq6lrPwcdp4IIKswVUwyE0ZiwhlpeOwRjNrvUX1yPrxr0dY8a0w8ePsc1DG8HAlZce8a0hZiWylMqu23d/vfzRFuA==
        

Рассмотрим последовательность действий, которые требуется совершить при обращении к функциям интеграторского интерфейса Диадока.

Первым делом, клиент Диадока должен получить авторизационный токен, используя команду :doc:`../http/Authenticate`.

При этом в параметре *ddauth_api_client_id* HTTP-заголовка ``Authorization`` требуется передать полученный в процессе регистрации ключ разработчика.

Соответствующий HTTP-запрос выглядит следующим образом:

::

    POST /Authenticate HTTP/1.1
    Host: diadoc-api.kontur.ru
    Authorization: DiadocAuth ddauth_api_client_id=testClient-8ee1638deae84c86b8e2069955c2825a
    Content-Length: 1252
    Connection: Keep-Alive

    <Двоичное DER-представление X.509-сертификата пользователя>
        
Также можно получить авторизационный токен с помощью логина и пароля, соответствующий запрос будет выглядеть следующим образом:

::

    POST /Authenticate?login=user@skbkontur.ru&password=qwerty HTTP/1.1
    Host: diadoc-api.kontur.ru
    Authorization: DiadocAuth ddauth_api_client_id=testClient-8ee1638deae84c86b8e2069955c2825a
    Content-Length: 1252
    Connection: Keep-Alive

В случае если вы пытаетесь получить токен с помощью сертификата, успешный ответ сервера будет выглядеть так:
::

    HTTP/1.1 200 OK
    Content-Length: 598

    <Двоичное DER-представление зашифрованного авторизационного токена>
        
В случае если вы пытаетесь получить токен по логину и паролю, успешный ответ сервера будет выглядеть так:
::

    HTTP/1.1 200 OK
    Content-Length: 598

    <Авторизационный токен>

Чтобы получить авторизационный токен по сертификату, клиент должен расшифровать тело ответа команды :doc:`../http/Authenticate` при помощи закрытого ключа, соответствующего пользовательскому сертификату. Полученный массив байтов нужно закодировать в :rfc:`Base64 <3548>` - строку. 

И далее к каждому HTTP-запросу к Диадоку требуется добавлять HTTP-заголовок ``Authorization`` с параметрами *ddauth_api_client_id=* и *ddauth_token=*.

Например, команда получения списка доступных пользователю ящиков транслируется в следующий HTTP-запрос:
::

    POST /GetMyOrganizations HTTP/1.1
    Host: diadoc-api.kontur.ru
    Authorization: DiadocAuth ddauth_api_client_id=testClient-8ee1638deae84c86b8e2069955c2825a,ddauth_token=3IU0iPhuhHPZ6lrlumGz4pICEedhQ1XmlMN1Pk8z0DJ51MXkcTi6Q3CODCC4xTMsjPFfhK6XM4kCJ4JJ42hlD499/Ui5WSq6lrPwcdp4IIKswVUwyE0ZiwhlpeOwRjNrvUX1yPrxr0dY8a0w8ePsc1DG8HAlZce8a0hZiWylMqu23d/vfzRFuA==
        
Для команд, предусматривающих работу с определенным ящиком (таких как получение и отправка сообщений), контроль доступа к ящику работает по следующему алгоритму:

1.  Из HTTP-заголовка Authorization текущего запроса извлекается значение параметра *ddauth_token*. Это значение декодируется и из него извлекается идентификатор пользователя.

  #.  Если какое-то из вышеперечисленных действий не удалось выполнить (например, в запросе отсутствует HTTP-заголовок ``Authorization``, или в этом заголовке отсутствует параметр *ddauth_token*, или значение этого параметра представляет собой поврежденный или просроченный токен и т.д.), то возвращается код ошибки 401 (Unauthorized).
  #.  Если в запросе был указан некорректный *ddauth_api_client_id*, то также возвращается код ошибки 401 (Unauthorized).

2.  По идентификатору пользователя находится множество ящиков, к которым данный пользователь имеет доступ. Это тот же самый список, которое возвращает метод :doc:`../http/GetMyOrganizations`.
3.  Из параметров текущего запроса извлекается идентификатор ящика. Если идентификатор ящика не принадлежит списку, полученному на предыдущем шаге, то возвращается код ошибки 403 (Forbidden).
4.  Иначе доступ разрешается.

Авторизационные токены можно на некоторое время кэшировать. То есть вовсе не обязательно вызывать метод :doc:`../http/Authenticate` перед каждым обращением к методам API Диадока. Рекомендуемая стратегия заключается в получении токена на сеанс работы пользователя/программы и повторном использовании его в течение одного сеанса.

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
