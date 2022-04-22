EmployeePowerOfAttorney
=======================

Структура ``EmployeePowerOfAttorney`` предназначена для хранения информации о машиночитаемой доверенности (МЧД), привязанной к сотруднику.

.. code-block:: protobuf

    message EmployeePowerOfAttorney {
        required PowerOfAttorney PowerOfAttorney = 1;
        required bool IsDefault = 2;
    }

- ``PowerOfAttorney`` — информация о доверенности, представленная структурой :doc:`PowerOfAttorney`.
- ``IsDefault`` — флаг, указывающий, является ли данная МЧД доверенностью по умолчанию.

----

.. rubric:: Использование

Структура ``EmployeePowerOfAttorney`` используется:

- в структуре ``EmployeePowerOfAttorneyList``, возвращаемой методом :doc:`../http/GetEmployeePowersOfAttorney`
- в теле ответа метода :doc:`../http/AddEmployeePowerOfAttorney`
- в теле ответа метода :doc:`../http/UpdateEmployeePowerOfAttorney`