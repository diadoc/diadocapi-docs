PowerOfAttorneyInfo
===================

Структура ``PowerOfAttorneyInfo`` предназначена для хранения информации о машиночитаемой доверенности (МЧД) и статусе ее проверки.

.. code-block:: protobuf

    message PowerOfAttorneyInfo {
        required PowerOfAttorneyFullId FullId = 1;
        optional PowerOfAttorneyValidationStatus Status = 2;
    }
   
- ``FullId`` — идентификатор МЧД, представленный структурой :doc:`PowerOfAttorneyFullId`.
- ``Status`` — статус проверки МЧД, представленный структурой :doc:`PowerOfAttorneyValidationStatus`.

----

.. rubric:: Использование

Структура ``PowerOfAttorneyInfo`` используется внутри структуры :doc:`Entity message`.
