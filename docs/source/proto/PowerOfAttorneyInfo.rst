PowerOfAttorneyInfo
===================

Структура ``PowerOfAttorneyInfo`` хранит информацию о машиночитаемой доверенности (МЧД) и статусе ее проверки.

.. code-block:: protobuf

    message PowerOfAttorneyInfo {
        required PowerOfAttorneyFullId FullId = 1;
        optional PowerOfAttorneyValidationStatus Status = 2;
        optional RoamingSendingStatus SendingStatus = 3;
        optional PowerOfAttorneySendingType SendingType = 4;
    }

- ``FullId`` — идентификатор МЧД. Представлен структурой :doc:`PowerOfAttorneyFullId`.
- ``Status`` — статус проверки МЧД. Представлен структурой :doc:`PowerOfAttorneyValidationStatus`.
- ``SendingStatus`` — статус отправки МЧД в роуминг. Представлен структурой :doc:`RoamingSendingStatus`.
- ``SendingType`` — способ передачи МЧД. Принимает значения из перечисления :doc:`PowerOfAttorneySendingType`.


----

.. rubric:: См. также

*Структура используется:*
	- в структуре :doc:`Entity message`

*Инструкции:*
	- :doc:`../instructions/powerofattorney`