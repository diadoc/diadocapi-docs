PowerOfAttorneyFullId
=====================

Структура ``PowerOfAttorneyFullId`` предназначена для хранения идентификатора машиночитаемой доверенности (МЧД).

.. code-block:: protobuf

    message PowerOfAttorneyFullId {
        required string RegistrationNumber = 1;
        required string IssuerInn = 2;
    }
   
- ``RegistrationNumber`` — регистрационный номер МЧД в формате GUID.
- ``IssuerInn`` — ИНН доверителя из МЧД.

----

.. rubric:: См. также

*Структура используется:*
	- в структуре :doc:`PowerOfAttorney`
	- в структуре :doc:`PowerOfAttorneyInfo`
	- в структуре :doc:`PowerOfAttorneyToPost`
	- в структуре :doc:`PowerOfAttorneyToRegister`
	- в структуре :doc:`SignaturePowerOfAttorney`

*Руководства:*
	- :doc:`../instructions/powerofattorney`