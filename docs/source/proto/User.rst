User
====

.. code-block:: protobuf

    message User {
        optional string Id = 1;
        optional string LastName = 2;
        optional string FirstName = 3;
        optional string MiddleName = 4;
        repeated CloudCertificate CloudCertificates = 5;
    }
        
    message CloudCertificate {
        required string Thumbprint = 1;
        required sfixed64 ValidFrom = 2;
        required sfixed64 ValidTo = 3;
    }
    
Информация о пользователе.

-  *Id* - Идентификатор пользователя в системе;

-  *LastName* - Фамилия;

-  *FirstName* - Имя;

-  *MiddleName* - Отчество;

-  *CloudCertificates* - список облачных сертификатов, доступных данному пользователю;

Информация об облачном сертификате.

-  *Thumbprint* - отпечаток сертификата;

-  *ValidFrom* - дата начала действия сертификата (ticks);

-  *ValidTo* - дата окончания действия сертификата (ticks);

