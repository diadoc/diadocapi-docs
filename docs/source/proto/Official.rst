Official
========

.. code-block:: protobuf

    message Official {
        required string Surname = 1;
        required string FirstName = 2;
        optional string Patronymic = 3;
        optional string JobTitle = 4;
    }

    message Attorney {
        optional string Date = 1;
        optional string Number = 2;
        optional string IssuerOrganizationName = 3;
        optional Official IssuerPerson = 4;
        optional string IssuerAdditionalInfo = 5;
        optional Official RecipientPerson = 6;
        optional string RecipientAdditionalInfo = 7;
    }
        

Структура данных Official представляет информацию о должностном лице:

-  Surname - фамилия должностного лица.

-  FirstName - имя должностного лица.

-  Patronymic - отчество должностного лица (необязательно).

-  JobTitle - название должности (необязательно).

Структура данных Attorney представляет информацию о доверенности:

-  Date - дата выдачи доверенности в формате ДД.ММ.ГГГГ.

-  Number - номер доверенности.

-  IssuerOrganizationName - название организации, представитель которой выдал доверенность.

-  IssuerPerson - должностное лицо, выдавшее доверенность.

-  IssuerAdditionalInfo - дополнительная информация о лице, выдавшем доверенность.

-  RecipientPerson - должностное лицо, получившее доверенность.

-  RecipientAdditionalInfo - дополнительная информация о лице, получившем доверенность.
