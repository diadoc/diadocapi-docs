User
====

.. code-block:: protobuf

    message User {
        optional string Id = 1;
        optional string LastName = 2;
        optional string FirstName = 3;
        optional string MiddleName = 4;
    }
        
    message CertificateInfo {
        optional string Thumbprint = 1;
        optional sfixed64 ValidFrom = 2;
        optional sfixed64 ValidTo = 3;
        optional string OrganizationName = 4;
        optional string Inn = 5;
    }
    
Информация о пользователе.

-  *Id* - Идентификатор пользователя в системе;

-  *LastName* - Фамилия;

-  *FirstName* - Имя;

-  *MiddleName* - Отчество.
