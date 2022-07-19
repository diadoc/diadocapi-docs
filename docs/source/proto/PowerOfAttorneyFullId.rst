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

.. rubric:: Использование

Структура ``PowerOfAttorneyFullId`` используется в структурах:

- :doc:`PowerOfAttorneyToRegister`
- :doc:`PowerOfAttorney`
- :doc:`PowerOfAttorneyToPost`
- :doc:`PowerOfAttorneyInfo`
- :doc:`SignaturePowerOfAttorney`
