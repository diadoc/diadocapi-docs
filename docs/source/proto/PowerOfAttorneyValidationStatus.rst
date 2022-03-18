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
        UnknownSeverity = 0; // reserved for backward compatibility
        Info = 1;
        Success = 2;
        Warning = 3;
        Error = 4;
    }
  
    enum PowerOfAttorneyValidationStatusNamedId {
        UnknownStatus = 0; // reserved for backward compatibility
        CanNotBeValidated = 1;
        IsValid = 2;
        IsNotValid = 3;
        ValidationError = 4;
    }
  
    message PowerOfAttorneyValidationError {
        required string Code = 1;
        required string Text = 2;
    }

- ``Severity`` — критичность статуса, значение из перечисления ``Severity``.
- ``StatusNamedId`` — текстовый идентификатор статуса, значение из перечисления ``PowerOfAttorneyValidationStatusNamedId``.
- ``StatusText`` — удобочитаемый текст статуса.
- ``Errors`` — список ошибок, представленных структурой ``PowerOfAttorneyValidationError`` с полями:

	- ``Code`` — код ошибки.
	- ``Text`` — текст ошибки.

----

.. rubric:: Использование

Структура ``PowerOfAttorneyValidationStatus`` используется:

- в структуре :doc:`PowerOfAttorneyInfo`
- в структуре :doc:`SignaturePowerOfAttorney`
- в структуре :doc:`DocflowStatusV3`
- в теле ответа метода :doc:`../http/PrevalidatePowerOfAttorney`

