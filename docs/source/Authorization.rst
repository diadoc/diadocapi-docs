Авторизация
===========

.. contents:: :local:
	:depth: 3

Чтобы работать с API Диадока, нужно авторизоваться. Сейчас Диадок поддерживает две схемы авторизации:

	- :ref:`с помощью OpenID Connect <auth_oidc>` — рекомендуемый способ аутентификации;
	- :ref:`с помощью методов Диадока <auth_authenticate>` — нерекомендуемый устаревший способ авторизации.


.. _auth_oidc:

Аутентификация через OpenID Connect
-----------------------------------

Диадок предоставляет возможность аутентифицироваться в продукте по протоколу `OpenID Connect <https://openid.net/connect/>`__. Для этого:

1. Оставьте заявку на `странице интеграции <https://www.diadoc.ru/integrations/api>`__. После этого с вами свяжется менеджер и предоставит вам доступ в `Кабинет интегратора <https://integrations.testkontur.ru/)>`__. Там вы сможете получить:

	- идентификатор приложения ``client_id``;
	- ключ приложения ``client_secret`` — секретный ключ, не передавайте его третьим лицам.

2. :ref:`Получите авторизационный токен <auth_get_token>` ``access_token``, используя ``client_id`` и ``client_secret``.
3. Используйте авторизационный токен ``access_token`` в заголовке ``Authorization`` при вызовах методов API Диадока:

   ::

    Authorization: Bearer <access_token>

4. :ref:`Обновите авторизационный токен <auth_refresh_token>` ``access_token`` до истечении времени жизни.

Для некоторых языков разработки в открытом доступе существуют готовые библиотеки или реализации интеграции с OpenID Connect: например, `JS <https://www.npmjs.com/package/oidc-client>`__, `.Net <https://www.nuget.org/packages/Microsoft.AspNetCore.Authentication.OpenIdConnect>`__ и `Java <https://mvnrepository.com/artifact/org.springframework.security/spring-security-openid>`__

Примеры реализации аутентификации через OpenID Connect в клиентском приложении можно найти по следующим ссылкам:
	- `ASP.NET Core приложение с OIDC-аутентификацией <https://git.skbkontur.ru/diadoc/integration-samples/-/tree/master/Diadoc.Integration/SampleWebApp.Oidc>`__
	- `Express.js приложение с OIDC-аутентификацией на базе express-openid-connect <https://git.skbkontur.ru/diadoc/integration-samples/-/tree/master/js/express-openid>`__

.. note::
	Подробная информация о порядке работы с OpenId Connect приведена на странице :doc:`oidc`.


.. _auth_get_token:

Получение токена
~~~~~~~~~~~~~~~~

Чтобы получить авторизационный токен ``access_token``, выполните следующие шаги:

1. Получите временный код авторизации ``authorization_code``.

   Для этого перенаправьте пользователя из интеграционного решения на страницу авторизации ``Authorization Endpoint`` с помощью запроса в сервис OpenID Провайдера.

   .. collapse:: Описание запроса

		**Параметры запроса**

		Все передаваемые параметры должны быть в формате url_encoded.

		``Content-type: application/x-www-form-urlencoded``
		
		- ``response_type`` — ответ, который нужно получить от OpenID Провайдера. Укажите значение ``code``.
		- ``client_id`` — идентификатор приложения, выданный при его регистрации.
		- ``scope`` — список прав доступа, которые необходимы приложению в текущей сессии. Укажите следующие значения для доступа к данным Диадока:

			- ``Diadoc.PublicAPI.Staging`` — для работы с тестовым пространством Диадока;
			- ``Diadoc.PublicAPI`` — для работы с продуктовым пространством Диадока.

		- ``redirect_uri`` — ссылка, на которую будет перенаправлен пользователь после аутентификации.
		- ``nonce`` — строка, предназначенная для проверки того, что запрос связан с будущим ``Access Token``. Она должна вернутся при получении ``Access Token``.

		**Пример запроса**

		::

			http://identity.testkontur.ru/connect/authorize?
				response_type=code
				&scope=openid Diadoc.PublicAPI.Staging
				&client_id=yourClientId
				&redirect_uri=http://www.example.com/
				&state=af0ifjsldkj
				&nonce=n-0S6_WzA2Mj

		**Ответ**

		OpenID Провайдер перенаправит пользователя на адрес, указанный в параметре ``redirect_uri`` с кодом подтверждения ``code``, и вернет временный код авторизации ``authorization_code``.

2. Обменяйте временный код авторизации ``authorization_code`` на ``access_token``.

   Для этого выполните запрос на ``Token Endpoint`` сервиса OpenID Провайдера.

   .. collapse:: Описание запроса

		**Параметры запроса**

		Все передаваемые параметры должны быть в формате url_encoded.

		``Content-type: application/x-www-form-urlencoded``

		- ``grant_type`` — способ запроса токена. Укажите значение ``authorization_code``.
		- ``authorization_code`` — временный код авторизации, полученный в запросе аутентификации.
		- ``client_id`` — идентификатор приложения, выданный при его регистрации.
		- ``client_secret`` — ключ приложения, выданный при его регистрации.
		- ``redirect_uri`` — ссылка, на которую получен код подтверждения.

		**Пример запроса**

		::

			POST /token
			Content-type: application/x-www-form-urlencoded

			grant_type=authorization_code
			code=SplxlOBeZQQYbYS6WxSbIA
			client_id=yourClientId
			client_secret=yourClientSecret
			redirect_uri=http://www.example.com

		**Ответ**

		В ответе метод вернет ``access_token`` и ``refresh_token``, который необходим для :ref:`обновления токена <auth_refresh_token>` ``access_token`` по истечении срока его жизни. Срок жизни ``access_token`` будет указан в ответе в поле ``expires_in``.

		**Пример ответа**

		::

			200 OK
			Content-type: application/json

			{
			    "access_token": "AAAAAAAAAAAAAAAAA",
			    "token_type": "Bearer",
			    "expires_in": 3600,
			    "id_token": "eyJhbGciOifQ.ewogI3pAKfQ.ggW8hq-rvKMzqg"
			}

.. note::
	Подробная инструкция по получению токена приведена в `документации OpenID Провайдера <https://developer.kontur.ru/Docs/html/schemes/auth_and_authorize.html#rst-murkup-authorize-by-code>`__.


.. _auth_refresh_token:

Обновление токена
~~~~~~~~~~~~~~~~~

Время жизни авторизационного токена ``access_token`` — 24 часа. До истечения этого времени его нужно обновить, иначе методы API будут возвращать ошибки, а пользователю вновь придется авторизовываться в OpenID Провайдере.

Отследить, когда закончится время жизни ``access_token``, можно по значению поля ``expires_in``, полученного вместе с токеном.

Чтобы обновить авторизационный токен ``access_token``, используйте ``refresh_token``, полученный вместе с ним при запросе. Для этого в интеграционном решении выполните запрос на Token Endpoint сервиса OpenID Провайдера.

Время жизни ``refresh_token`` — 30 суток. После этого пользователю придется снова авторизовываться в OpenID Провайдере.

.. collapse:: Описание запроса

	**Параметры запроса**

	- ``grant_type`` — способ запроса токена. Укажите значение ``refresh_token``.
	- ``client_id`` — идентификатор приложения, выданный при его регистрации.
	- ``client_secret`` — ключ приложения, выданный при его регистрации.
	- ``refresh_token`` — токен, полученный в результате запроса на ``Token Endpoint``.

	**Пример запроса**

	::

		POST /token
		Content-type: application/x-www-form-urlencoded

		grant_type=refresh_token
		&client_id=yourClientId
		&client_secret=yourClientSecret
		&refresh_token=1487e3f7ce5aea612e2d7727ded76ad574e30643046ae2c247ae9c94c6b61e71

	**Пример ответа**

	::

		200 OK
		Content-type: application/json

		{
		    "access_token": "811d583cf85deb7ab67bd91b96a9a4bafb63d6a062d7dd72f81601b84c19dc40",
		    "expires_in": 86400,
		    "token_type": "Bearer",
		    "refresh_token": "fd672752f8e9c4a8eb083fb2375b3126ae37dc69a0cf46953ef9a6e3f5a692df"
		}


.. note::
	Подробная инструкция по обновлению токена приведена на странице `Обновление Access Token <https://developer.kontur.ru/Docs/html/schemes/using_refresh.html>`__.


.. _auth_authenticate:

Авторизация через методы Диадока
--------------------------------

.. warning::
	Способ авторизации с помощью методов API Диадока является устаревшим и не рекомендуется к использованию. Используйте вместо него :ref:`авторизацию через OpenID Connect <auth_oidc>`.

Для авторизации с помощью методов API нужна следующая информация:

	- ключ разработчика — уникальный идентификатор интегратора в формате GUID. Чтобы получить ключ разработчика, оставьте заявку на `странице интеграции <https://www.diadoc.ru/integrations/api>`__. Не передавайте свой ключ третьим лицам.
	- авторизационный токен — массив байтов, однозначно идентифицирующий пользователя.

Эту информацию нужно передавать в стандартном HTTP-заголовке ``Authorization`` в соответствии со схемой аутентификации Диадока ``DiadocAuth`` со следующими параметрами:

	- ``ddauth_api_client_id`` — определяет ключ разработчика,
	- ``ddauth_token`` — определяет авторизационный токен.

Значения параметров в заголовке отделяются от их имен символами «=», параметры разделяются символами «,». Например:

::

    Authorization: DiadocAuth
    ddauth_api_client_id=testClient-8ee1638deae84c86b8e2069955c2825a,
    ddauth_token=3IU0iPhuhHPZ6lrlumGz4pICEedhQ1XmlMN1Pk8z0DJ51MXkcTi6Q3CODCC4xTMsjPFfhK6XM4kCJ4JJ42hlD499/Ui5WSq6lrPwcdp4IIKswVUwyE0ZiwhlpeOwRjNrvUX1yPrxr0dY8a0w8ePsc1DG8HAlZce8a0hZiWylMqu23d/vfzRFuA==

..

Получение авторизационного токена
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Подробная информация обо всех способах получения токена приведена на странице метода :doc:`http/obsolete/Authenticate`.

При вызове метода ``Authenticate`` в параметре ``ddauth_api_client_id`` HTTP-заголовка ``Authorization`` передайте ключ разработчика.

Необязательно вызывать метод :doc:`http/obsolete/Authenticate` перед каждым обращением к методам API Диадока — авторизационные токены можно кэшировать. Мы рекомендуем сохранить и использовать полученный токен в течение всего сеанса работы. Полученный токен остается действительным в течение 24 часов.

Авторизация при вызове методов API
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Ключ разработчика и полученный авторизационный токен нужно передавать в каждый метод API. Для этого при вызове методов API нужно к каждому запросу добавлять HTTP-заголовок ``Authorization`` с параметрами ``ddauth_api_client_id`` и ``ddauth_token``. Например, HTTP-запрос на получение списка доступных пользователю ящиков будет выглядеть так:

::

    POST https://diadoc-api.kontur.ru/GetMyOrganizations HTTP/1.1
    Host: diadoc-api.kontur.ru
    Authorization: DiadocAuth ddauth_api_client_id=testClient-8ee1638deae84c86b8e2069955c2825a,ddauth_token=3IU0iPhuhHPZ6lrlumGz4pICEedhQ1XmlMN1Pk8z0DJ51MXkcTi6Q3CODCC4xTMsjPFfhK6XM4kCJ4JJ42hlD499/Ui5WSq6lrPwcdp4IIKswVUwyE0ZiwhlpeOwRjNrvUX1yPrxr0dY8a0w8ePsc1DG8HAlZce8a0hZiWylMqu23d/vfzRFuA==

Проверка прав пользователя
~~~~~~~~~~~~~~~~~~~~~~~~~~

Методы, работающие с определенным ящиком, контролируют доступ к нему по следующему алгоритму:

1. Сервер Диадока извлекает из HTTP-заголовка ``Authorization`` значение параметра ``ddauth_token``. После его декодирования сервер получает идентификатор пользователя. Если какое-то действие не удалось выполнить, метод вернет код ошибки ``401 (Unauthorized)``. Это возможно в случаях, когда:

 - в запросе отсутствует HTTP-заголовок ``Authorization``,
 - нет параметра ``ddauth_token``,
 - токен поврежден или просрочен,
 - указан некорректный ``ddauth_api_client_id``.

2. По идентификатору пользователя Диадок находит ящики, к которым у пользователя есть доступ. Список ящиков совпадает со списком, который вернет метод :doc:`http/GetMyOrganizations`.
3. Сервер извлекает идентификатор ящика из параметров запроса. Если идентификатор ящика не входит в список ящиков, доступных пользователю, метод вернет код ошибки ``403 (Forbidden)``.


.. toctree::
	:hidden:

	oidc

----

.. rubric:: См. также

*Инструкции:*
	- :doc:`oidc`

*Методы для аутентификации:*
    - :doc:`http/obsolete/Authenticate` — аутентифицирует пользователя в Диадоке
    - :doc:`http/obsolete/AuthenticateConfirm` — возвращает авторизационный токен при аутентификации по сертификату