PowerOfAttorneyInfo
===================

Структура ``PowerOfAttorneyInfo`` хранит информацию о машиночитаемой доверенности (МЧД) и статусе ее проверки.

.. code-block:: protobuf

    message PowerOfAttorneyInfo {
        required PowerOfAttorneyFullId FullId = 1;
        optional PowerOfAttorneyValidationStatus Status = 2;
        optional RoamingSendingStatus SendingStatus = 3;
    }
   
- ``FullId`` — идентификатор МЧД, представленный структурой :doc:`PowerOfAttorneyFullId`.
- ``Status`` — статус проверки МЧД, представленный структурой :doc:`PowerOfAttorneyValidationStatus`.
- ``SendingStatus`` — статус отправки МЧД в роуминг, представленный структурой :doc:`RoamingSendingStatus`.

----

.. rubric:: Смотри также

*Структура используется:*
	- в структуре :doc:`Entity message`.
	
*Руководства:*
	- :doc:`Как работать с МЧД <../howto/powerofattorney>`