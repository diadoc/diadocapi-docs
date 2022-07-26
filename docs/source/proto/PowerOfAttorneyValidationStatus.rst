PowerOfAttorneyValidationStatus
===============================

Структура ``PowerOfAttorneyValidationStatus`` предназначена для хранения информации о статусе проверки машиночитаемой доверенности (МЧД).

.. code-block:: protobuf

    message PowerOfAttorneyValidationStatus {
        optional Severity Severity = 1 [default = UnknownSeverity];
        optional PowerOfAttorneyValidationStatusNamedId StatusNamedId = 2 [default = UnknownStatus];
        optional string StatusText = 3;
        repeated PowerOfAttorneyValidationError Errors = 4;
    }
 
    enum Severity {
        UnknownSeverity = 0;
        Info = 1;
        Success = 2;
        Warning = 3;
        Error = 4;
    }
  
    enum PowerOfAttorneyValidationStatusNamedId {
        UnknownStatus = 0;
        CanNotBeValidated = 1;
        IsValid = 2;
        IsNotValid = 3;
        ValidationError = 4;
    }
  
    message PowerOfAttorneyValidationError {
        required string Code = 1;
        required string Text = 2;
    }

- ``Severity`` — критичность статуса, значение из перечисления ``Severity``:

		- ``UnknownSeverity`` — значение по умолчанию;
		- ``Info`` — информация;
		- ``Success`` — успешно;
		- ``Warning`` — предупреждение;
		- ``Error`` — ошибка.

- ``StatusNamedId`` — текстовый идентификатор статуса, значение из перечисления ``PowerOfAttorneyValidationStatusNamedId``:

		- ``UnknownStatus`` — значение по умолчанию;
		- ``CanNotBeValidated`` — не получилось выполнить проверку из-за ошибки валидации МЧД;
		- ``IsValid`` — все проверки выполнены без ошибок;
		- ``IsNotValid`` — среди МЧД есть хотя бы одна невалидная; 
		- ``ValidationError`` — при проверке возникли ошибки валидации.

- ``StatusText`` — удобочитаемый текст статуса.
- ``Errors`` — список ошибок, представленных структурой ``PowerOfAttorneyValidationError`` с полями:

	- ``Code`` — код ошибки.
	- ``Text`` — текст ошибки.

----

.. rubric:: Смотри также

*Структура используется:*
	- в структуре :doc:`PowerOfAttorneyInfo`,
	- в структуре :doc:`SignaturePowerOfAttorney`,
	- в структуре :doc:`DocflowStatusV3`,
	- в теле ответа метода :doc:`../http/PrevalidatePowerOfAttorney`.

*Инструкции:*
	- :doc:`Как работать с МЧД <../howto/powerofattorney>`