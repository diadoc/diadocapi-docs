Address
=======

Структура ``Address`` представляет собой информацию об адресе организации.

.. code-block:: protobuf

    message Address {
        optional RussianAddress RussianAddress = 1;
        optional ForeignAddress ForeignAddress = 2;
        optional string AddressCode = 3;
    }

    message RussianAddress {
        optional string ZipCode = 1;
        required string Region = 2;
        optional string Territory = 3;
        optional string City = 4;
        optional string Locality = 5;
        optional string Street = 6;
        optional string Building = 7;
        optional string Block = 8;
        optional string Apartment = 9;
        optional string OtherInformation = 10;
    }

    message ForeignAddress {
        required string Country = 1;
        required string Address = 2;
    }


Обязательно должно быть заполнено одно из полей ``RussianAddress`` или ``ForeignAddress``.

- ``RussianAddress`` — российский адрес организации, представленный структурой ``RussianAddress`` с полями:

	- ``ZipCode`` — индекс.
	- ``Region`` — код региона.
	- ``Territory`` — район.
	- ``City`` — город.
	- ``Locality`` — населенный пункт.
	- ``Street`` — улица.
	- ``Building`` — дом.
	- ``Block`` — корпус.
	- ``Apartment`` — квартира.
	- ``OtherInformation`` — иные сведения.

- ``ForeignAddress`` — иностранный адрес организации, представленный структурой ``ForeignAddress`` с полями:

	- ``Country`` — код страны.
	- ``Address`` — текст адреса.

- ``AddressCode`` — код ГАР.

----

.. rubric:: См. также

*Структура используется:*
	- в структуре :doc:`obsolete/ExtendedOrganizationInfo`
	- в структуре :doc:`Department`
	- в структуре :doc:`Departments/DepartmentToCreate`
	- в структуре :doc:`Organization`