PowerOfAttorneyToUpdate
=======================

Структура ``PowerOfAttorneyToUpdate`` используется для :doc:`обновления <../http/UpdatePowerOfAttorney>` настроек машиночитаемой доверенности (МЧД) для сотрудника.

.. code-block:: protobuf

    message EmployeePowerOfAttorneyToUpdate {
        optional EmployeePowerOfAttorneyIsDefaultPatch IsDefaultPatch = 1;
    }

    message EmployeePowerOfAttorneyIsDefaultPatch {
        required bool IsDefault = 1;
    }

- ``IsDefaultPatch`` — структура ``EmployeePowerOfAttorneyIsDefaultPatch``, управляющая флагом «Использовать по умолчанию» для МЧД, с полями:
	
	- ``IsDefault`` - флаг «Использовать по умолчанию».

----

.. rubric:: Использование

Структура ``PowerOfAttorneyToUpdate`` используется в теле запроса метода :doc:`../http/UpdateEmployeePowerOfAttorney`.