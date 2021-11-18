Authenticate
============

.. contents::
   :local:


Authenticate v3
---------------

.. http:post:: /V3/Authenticate

    :reqheader Authorization: данные, необходимые для :doc:`авторизации <../Authorization>`
    
    :query type: Параметр type обозначает метод, которым пользователь хочет аутентифицироваться. Параметр не может быть пустым и принимает значения

    :statuscode 200: операция успешно завершена;
    :statuscode 400: данные в запросе имеют неверный формат или отсутствуют обязательные параметры;
    :statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization``, или в этом заголовке отсутствует параметр *ddauth_api_client_id*, или переданный в нем ключ разработчика не зарегистрирован в Диадоке;
    :statuscode 405: используется неподходящий HTTP-метод;
    :statuscode 500: при обработке запроса возникла непредвиденная ошибка.
    
Параметр *type* может принимать значения:
    
    + password - логин и пароль
    + sid - `auth.sid <https://docs-ke.readthedocs.io/ru/latest/auth/auth.sid.html>`__ из API Аутентификатора
    + certificate - сертификат
    + trust - доверительная аутентификаци

В версии v3 от передаваемого параметра *type* зависит тело запроса.

- **Аутентификация по логину и паролю** :
    
Необходимо указывать type - password, и в теле запроса передавать сериализованный объект.
Возможно передавать данные в формате json, в этом случае необходимо указать заголовок *Content-Type: application/json*

.. code-block:: json 
   
    { 
        "login" : "login", 
        "password" : "pass" 
    }

Либо передавать в формате protobuf. В этом случае Content-Type указывать не обязательно, так как по умолчанию десериализация происходит из protobuf.

.. code-block:: protobuf

    message LoginPassword {
        required string Login = 1;
        required string Password = 2;
    }

- **Аутентификация по auth.sid API аутентификатора** :

Необходимо указать type - sid, в теле запроса передавая `auth.sid <https://docs-ke.readthedocs.io/ru/latest/auth/auth.sid.html>`__ c заголовком *Content-Type: text/plain*

- **Аутентификация по сертификату**:

Необходимо указать type - certificate, в тело запроса передать бинарное содержимое открытого ключа сертификата c заголовком 
*Content-Type: application/octet-stream*.

В ответе метода возвращается зашифрованная строка. Полученный ответ следует расшифровать закрытым ключом сертификата. Расшифрованный файл надо декодировать, преобразовать все символы полученной base64 строки в URL формат и передать результат на вход :doc:`AuthenticateConfirm`

- **Доверительная аутентификация**

Чтобы сохранить привязку(Binding) для доверительной аутентификации, необходимо авторизоваться с помощью пароля или сертификата, с указанием заголовков:

    + X-Diadoc-ServiceKey (ServiceKey)
    + X-Diadoc-ServiceUserId (ServiceUserId)

Чтобы воспользоваться доверительной аутентификацией, необходимо указать type - trust, с указанием заголовков X-Diadoc-ServiceKey, X-Diadoc-ServiceUserId, после создания привязки.

Authenticate v2
---------------

Метод устарел

Authenticate
------------

Метод устарел
