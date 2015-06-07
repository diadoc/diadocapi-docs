ExternalServiceAuthInfo
=======================

.. code-block:: protobuf

    message ExternalServiceAuthInfo {
         optional string ServiceUserId = 1;
         optional string Thumbprint = 2;
    }

Структура данных *ExternalServiceAuthInfo* представляет собой аутентификационную информацию, возвращаемую методом :doc:`../http/GetExternalServiceAuthInfo`.

Структура данных *ExternalServiceAuthInfo* содержит следующую информацию:

-  *ServiceUserId* - уникальный идентификатор пользователя во внешней системе;

-  *Thumbprint* - отпечаток сертификата пользователя.