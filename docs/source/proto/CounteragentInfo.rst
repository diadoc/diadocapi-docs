CounteragentInfo
================

Структура ``CounteragentInfo`` хранит информацию о :doc:`контрагенте <../entities/counteragent>`.

.. code-block:: protobuf

    message CounteragentInfo {
        required string CounteragentBoxId = 1;
        required CounteragentStatus Status = 2; 
        required sfixed64 EventTimestampTicks = 3;
        optional string LastEventComment = 4; 
        optional string MessageFromCounteragent = 5;
        optional string MessageToCounteragent = 6;
        optional DocumentId InvitationDocumentId = 7;
        optional string CounteragentGroupId = 8;
    }

- ``CounteragentBoxId`` — идентификатор ящика контрагента.
- ``Status`` — статус контрагента, принимает значения из перечисления :doc:`CounteragentStatus`.
- ``EventTimestampTicks`` — время последнего изменения статуса контрагента, представляет собой целое число тиков, прошедших с момента времени 00:00:00 01.01.0001.
- ``LastEventComment`` — текст сообщения из последнего события взаимодействия с контрагентом. Если статус контрагента ``CounteragentStatus = IsMyCounteragent``, то поле будет отстутствовать, а текст последнего сообщения будет отображаться в поле ``MessageFromCounteragent`` или ``MessageToCounteragent``.
- ``MessageFromCounteragent`` — текст сообщения, полученного от контрагента.
- ``MessageToCounteragent`` — текст сообщения, отправленнонго контрагенту.
- ``InvitationDocumentId`` — идентификатор документа, отправленного вместе с приглашением. Представлен структурой :doc:`DocumentId`.
- ``CounteragentGroupId`` — идентификатор группы, в которую добавлен контрагент.

----

.. rubric:: См. также

*Структура используется:*
	- в структуре :doc:`BoxCounteragentEvent <BoxCounteragentEventList>`

*Определение:*
	- :doc:`../entities/counteragent`

*Инструкции:*
	- :doc:`../instructions/counteragents`