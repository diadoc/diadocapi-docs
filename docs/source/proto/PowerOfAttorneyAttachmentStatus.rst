PowerOfAttorneyAttachmentStatus
===============================

Структура ``PowerOfAttorneyAttachmentStatus`` представляет собой статус приложенности машиночитаемой доверенности (МЧД) к подписи.

.. code-block:: protobuf

    message PowerOfAttorneyAttachmentStatus {
        required StatusName StatusName = 1;
        optional string Comment = 2;
    }

    enum StatusName
    {
        Unknown = 0;
        PowerOfAttorneyAttached = 1;
        PowerOfAttorneyNotRequired = 2;
        PowerOfAttorneyRequired = 3;
    }

- ``StatusName`` - значение статуса, принимает значение из перечисления ``StatusName``:

	- ``Unknown`` — значение не определено;
	- ``PowerOfAttorneyAttached`` — МЧД приложена;
	- ``PowerOfAttorneyNotRequired`` — МЧД не требуется;
	- ``PowerOfAttorneyRequired`` — МЧД требуется.

- ``Comment`` — комментарий к статусу, заполняется только для статуса ``PowerOfAttorneyRequired``.

----

.. rubric:: См. также

*Структура используется:*
	- в структуре :doc:`Entity message`
	- в структуре :doc:`SignatureV3`


*Инструкции:*
	- :doc:`../instructions/powerofattorney`