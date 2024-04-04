PowerOfAttorneyToUpdate
=======================

Структура ``PowerOfAttorneyToUpdate`` используется для :doc:`обновления<../http/UpdateEmployeePowerOfAttorney>` настроек машиночитаемой доверенности (МЧД) для сотрудника.

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

.. rubric:: См. также

*Структура используется:*
	- в теле запроса метода :doc:`../http/UpdateEmployeePowerOfAttorney`

*Руководства:*
	- :doc:`../howto/powerofattorney`