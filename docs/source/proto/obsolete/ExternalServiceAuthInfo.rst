ExternalServiceAuthInfo
=======================

.. warning::
	Эта структура удалена из API. Она возвращалась методом :doc:`../../http/obsolete/GetExternalServiceAuthInfo`.

.. code-block:: protobuf

    message ExternalServiceAuthInfo {
         optional string ServiceUserId = 1;
         optional string Thumbprint = 2;
    }

Структура данных *ExternalServiceAuthInfo* представляет собой аутентификационную информацию, возвращаемую методом :doc:`../../http/obsolete/GetExternalServiceAuthInfo`.

Структура данных *ExternalServiceAuthInfo* содержит следующую информацию:

-  *ServiceUserId* - уникальный идентификатор пользователя во внешней системе;

-  *Thumbprint* - отпечаток сертификата пользователя.