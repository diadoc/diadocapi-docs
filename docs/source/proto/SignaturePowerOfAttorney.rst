SignaturePowerOfAttorney
========================

Структура ``SignaturePowerOfAttorney`` предназначена для хранения информации о машиночитаемой доверенности (МЧД), использованной при подписании документа, и статусе ее проверки.

.. code-block:: protobuf

    message SignaturePowerOfAttorney {
        required Entity Entity = 1;
        required PowerOfAttorneyFullId FullId = 2;
        optional PowerOfAttorneyValidationStatus Status = 3;
        repeated PowerOfAttorneyStatusChange StatusChanges = 4;
    }

    message PowerOfAttorneyStatusChange (
        required Entity Entity = 1;
        required PowerOfAttorneyValidationStatus PowerOfAttorneyStatus = 2;
    }
   
- ``Entity`` — сущность, содержащая идентификатор МЧД и время ее создания, преставленная структурой :doc:`Entity`.
- ``FullId`` — идентификатор МЧД, представленный структурой :doc:`PowerOfAttorneyFullId`.
- ``Status`` — последний статус проверки МЧД, представленный структурой :doc:`PowerOfAttorneyValidationStatus`.
- ``StatusChanges`` — история статусов МЧД:

	- ``Entity`` — идентификатор и время установки статуса, преставленныя структурой :doc:`Entity`.
	- ``PowerOfAttorneyStatus`` — статус проверки МЧД, представленный структурой :doc:`PowerOfAttorneyValidationStatus`.

----

.. rubric:: Использование

Структура ``SignaturePowerOfAttorney`` используется внутри структуры :doc:`SignatureV3`.
