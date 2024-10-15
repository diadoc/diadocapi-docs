RoamingSendingStatus
====================

Структура ``RoamingSendingStatus`` хранит информацию о статусе отправки машиночитаемой доверенности (МЧД) в роуминг.

.. code-block:: protobuf

    message RoamingSendingStatus {
        optional Severity Severity = 1 [default = UnknownSeverity];
        optional RoamingSendingStatusNamedId StatusNamedId = 2 [default = UnknownStatus];
        optional string StatusText = 3;
        repeated RoamingSendingError Errors = 4;
    }

    enum RoamingSendingStatusNamedId {
        UnknownStatus = 0;
        IsSent = 1;
        SendingError = 2;
    }

    message RoamingSendingError {
        required string Code = 1;
        required string Text = 2;
    }

- ``Severity`` — критичность статуса, принимает значения из перечисления :doc:`Severity`.

- ``StatusNamedId`` — статус отправки МЧД в роуминг, принимает значения из перечисления ``RoamingSendingStatusNamedId``:

	- ``UnknownStatus`` — статус неизвестен. Возвращается, если клиент использует устаревшую версию SDK и не может интерпретировать информацию, переданную сервером;
	- ``IsSent`` — МЧД отправлена;
	- ``SendingError`` — ошибка отправки.

- ``StatusText`` — текст статуса.

- ``Errors`` — список ошибок отправки в роуминг. Возвращается, если ``StatusNamedId=SendingError``. Представлены структурой ``RoamingSendingError`` с полями:

	- ``Code`` — код ошибки.
	- ``Text`` — текст ошибки.


----

.. rubric:: См. также

*Структура используется:*
	- в структуре :doc:`DocflowStatusV3`
	- в структуре :doc:`PowerOfAttorneyInfo`
	- в структуре :doc:`SignaturePowerOfAttorney`