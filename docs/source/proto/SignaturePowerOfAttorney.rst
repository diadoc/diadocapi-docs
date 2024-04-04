SignaturePowerOfAttorney
========================

Структура ``SignaturePowerOfAttorney`` предназначена для хранения информации о машиночитаемой доверенности (МЧД), использованной при подписании документа, и статусе ее проверки.

.. code-block:: protobuf

    message SignaturePowerOfAttorney {
        required Entity Entity = 1;
        required PowerOfAttorneyFullId FullId = 2;
        optional PowerOfAttorneyValidationStatus Status = 3;
        repeated PowerOfAttorneyStatusChange StatusChanges = 4;
        optional RoamingSendingStatus SendingStatus = 5;
        optional PowerOfAttorneySendingType SendingType = 6;
    }

    message PowerOfAttorneyStatusChange {
        required Entity Entity = 1;
        required PowerOfAttorneyValidationStatus PowerOfAttorneyStatus = 2;
    }

- ``Entity`` — сущность, содержащая идентификатор МЧД и время ее создания. Представлена структурой :doc:`Entity`.
- ``FullId`` — идентификатор МЧД. Представлен структурой :doc:`PowerOfAttorneyFullId`.
- ``Status`` — последний статус проверки МЧД. Представлен структурой :doc:`PowerOfAttorneyValidationStatus`.
- ``StatusChanges`` — история статусов МЧД. Статусы представлены структурой ``PowerOfAttorneyStatusChange`` с полями:

	- ``Entity`` — идентификатор и время установки статуса, преставленные структурой :doc:`Entity`.
	- ``PowerOfAttorneyStatus`` — статус проверки МЧД, представленный структурой :doc:`PowerOfAttorneyValidationStatus`.

- ``SendingStatus`` — статус отправки МЧД в роуминг. Представлен структурой :doc:`RoamingSendingStatus`.
- ``SendingType`` — способ передачи МЧД. Принимает значения из перечисления :doc:`PowerOfAttorneySendingType`.

----

.. rubric:: См. также

*Структура используется:*
	- в структуре :doc:`SignatureV3`

*Руководства:*
	- :doc:`../howto/powerofattorney`
