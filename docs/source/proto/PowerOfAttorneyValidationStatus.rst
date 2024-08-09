PowerOfAttorneyValidationStatus
===============================

На этой странице, помимо ``PowerOfAttorneyValidationStatus``, описаны следующие структуры:

.. contents:: :local:


Структура ``PowerOfAttorneyValidationStatus`` предназначена для хранения информации о статусе проверки машиночитаемой доверенности (МЧД).

.. code-block:: protobuf

    message PowerOfAttorneyValidationStatus {
        required Severity Severity = 1;
        required PowerOfAttorneyValidationStatusNamedId StatusNamedId = 2;
        optional string StatusText = 3;
        repeated PowerOfAttorneyValidationError Errors = 4 [deprecated = true];
        optional ValidationProtocol ValidationProtocol = 5;
        optional PowerOfAttorneyValidationError OperationError = 6;
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
        IsNotAttached = 5;
        HasWarnings = 6;
    }


- ``Severity`` — критичность статуса, значение из перечисления ``Severity``:

		- ``UnknownSeverity`` — значение по умолчанию;
		- ``Info`` — информация;
		- ``Success`` — успешно;
		- ``Warning`` — предупреждение;
		- ``Error`` — ошибка.

- ``StatusNamedId`` — текстовый идентификатор статуса, значение из перечисления ``PowerOfAttorneyValidationStatusNamedId``:

		- ``UnknownStatus`` — значение по умолчанию;
		- ``CanNotBeValidated`` — не удалось передать МЧД на валидацию. Ошибка может возникнуть в случае, когда файл МЧД некорректный или из него не удалось получить необходимые данные для проверки — данные о доверенности, о доверителе, о представителе из подписи и т.п.;
		- ``IsValid`` — все проверки выполнены без ошибок;
		- ``IsNotValid`` — среди МЧД есть хотя бы одна невалидная;
		- ``ValidationError`` — МЧД была передана на валидацию, но во время выполнения проверок произошла внутренняя ошибка;
		- ``IsNotAttached`` — МЧД не приложена к подписи, возвращается только для общего (сводного) статуса МЧД;
		- ``HasWarnings`` — часть проверок не может быть выполнена или была выполнена с предупреждениями.

- ``StatusText`` — удобочитаемый текст статуса.
- ``Errors`` — поле устарело, используйте значение поля ``OperationError``.
- ``ValidationProtocol`` — протокол валидации с результатами выполнения проверок, представленный структурой :ref:`ValidationProtocol`. Возвращается в случае, когда ``StatusNamedId`` принимает значение:

	- ``IsValid``,
	- ``IsNotValid``,
	- ``HasWarnings``.

- ``OperationError`` — описание ошибки, произошедшей в процессе выполнения операции, представленное структурой :ref:`PowerOfAttorneyValidationError`. Возвращается в случае, если ``StatusNamedId`` принимает значение ``ValidationError`` или ``CanNotBeValidated``.


.. _ValidationProtocol:

ValidationProtocol
------------------

Структура ``ValidationProtocol`` представляет собой протокол валидации, содержащий результат выполнения проверок МЧД.

.. code-block:: protobuf

    message ValidationProtocol {
        repeated ValidationCheckResult CheckResults = 1;
    }

    message ValidationCheckResult {
        required string Status = 1;
        required string Name = 2;
        optional PowerOfAttorneyValidationError Error = 3;
    }

- ``CheckResults`` — результат проверки МЧД, представленный структурой ``ValidationCheckResult`` с полями:

	- ``Status`` — результат выполнения проверки.
	- ``Name`` — текстовый идентификатор проверки.
	- ``Error`` — информация об ошибке или предупреждении, представленная структурой :ref:`PowerOfAttorneyValidationError`.


.. _PowerOfAttorneyValidationError:

PowerOfAttorneyValidationError
------------------------------

Структура ``PowerOfAttorneyValidationError`` хранит информацию об ошибке, произошедшей при выполнении проверки МЧД.

.. code-block:: protobuf

    message PowerOfAttorneyValidationError {
        required string Code = 1;
        required string Text = 2;
    }

- ``Code`` — код ошибки.
- ``Text`` — текст ошибки.


----

.. rubric:: См. также

*Структура используется:*
	- в структуре :doc:`DocflowStatusV3`
	- в структуре :doc:`PowerOfAttorneyInfo`
	- в структуре :doc:`SignaturePowerOfAttorney`
	- в теле ответа метода :doc:`../http/PrevalidatePowerOfAttorney`

*Инструкции:*
	- :doc:`../instructions/powerofattorney`