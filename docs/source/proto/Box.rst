Box
===

Структура ``Box`` содержит информацию об одном :doc:`ящике <../entities/box>` организации.

.. code-block:: protobuf

    message Box {
        required string BoxId = 1;
        required string Title = 2;
        optional Organization Organization = 3;
        optional OrganizationInvoiceFormatVersion InvoiceFormatVersion = 4 [default = v5_02];
        optional bool EncryptedDocumentsAllowed = 5;
        required string BoxIdGuid = 6;
    }

    enum OrganizationInvoiceFormatVersion {
        v5_01 = 1;
        v5_02 = 2;
    }

- ``BoxId`` — идентификатор ящика.
- ``Title`` — наименование ящика.
- ``Organization`` — организация-владелец ящика. Заполнено только если структура ``Box`` возвращается методом :doc:`../http/GetBox`. В остальных случаях не заполняется, т.к. структура ``Box`` входит в состав структуры :doc:`Organization`.
- ``InvoiceFormatVersion`` — версия счета-фактуры, которая используется по умолчанию в данном ящике. Принимает значение из перечисления ``OrganizationInvoiceFormatVersion``:

	- ``v5_01`` — версия 01;
	- ``v5_02`` — версия 02.

- ``EncryptedDocumentsAllowed`` — признак того, что в ящик поддерживает отправку зашифрованных документов.
- ``BoxIdGuid`` — идентификатор ящика в формате GUID. Это значение нужно передавать в методы в качестве параметра запроса ``boxId``.

----

.. rubric:: См. также

*Структура используется:*
	- в структуре :doc:`Organization`
	- в теле ответа метода :doc:`../http/GetBox`
	- идентификатор ``BoxId`` используется при вызове многих методов API для указания ящика организации

*Определение:*
	- :doc:`../entities/box`