PowerOfAttorneyRegisterResult
=============================

Структура ``PowerOfAttorneyRegisterResult`` хранит данные о :doc:`результате регистрации <../http/RegisterPowerOfAttorneyResult>` машиночитаемой доверенности (МЧД).

.. code-block:: protobuf

    message PowerOfAttorneyRegisterResult {
        required string OperationStatus = 1;
        optional PowerOfAttorney PowerOfAttorney = 2;
        optional PowerOfAttorneyStatus Status = 3;
        repeated PowerOfAttorneyOperationError Errors = 4;
    }

    message PowerOfAttorneyStatus {
        required string Status = 1;
        optional Timestamp LastCheckAt = 2;
    }

    message PowerOfAttorneyOperationError {
        required string Code = 1;
        required string Text = 2;
    }

- ``OperationStatus`` — статус выполнения операции регистрации. Принимает значения:

	- ``Unknown`` — неизвестный статус;
	- ``Queued`` — операция в очереди;
	- ``Processing`` — операция выполняется;
	- ``Done`` — операция успешно завершена;
	- ``Error`` — ошибка при выполнении операции.

- ``PowerOfAttorney`` — информация о МЧД, представленная структурой :doc:`PowerOfAttorney`. Возвращается, если ``OperationStatus = Done``.
- ``Status`` — статус МЧД, представленный структурой ``PowerOfAttorneyStatus`` с полями:

	- ``Status`` — строка со статусом МЧД. Принимает значения:
	
		- ``created`` — создана, но еще не действует;
		- ``active`` — активна;
		- ``expired`` — срок действия истек;
		- ``revoked`` — отозвана.
		
	- ``LastCheckAt`` — дата последней проверки, если такая выполнялась. Представлена структурой :doc:`Timestamp`.
	
- ``Errors`` — список ошибок, которые возникли при регистрации МЧД. Возвращается, если ``OperationStatus = Error``. Каждый элемент списка представлен структурой ``PowerOfAttorneyOperationError`` с полями:

	- ``Code`` — код ошибки.
	- ``Text`` — текст ошибки.

----

.. rubric:: См. также

*Структура используется:*
	- в теле ответа метода :doc:`../http/RegisterPowerOfAttorneyResult`

*Руководства:*
	- :doc:`../instructions/powerofattorney`