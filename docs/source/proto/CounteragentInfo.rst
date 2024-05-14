CounteragentInfo
================

Структура ``CounteragentInfo`` содержит информацию о :doc:`контрагенте <../entities/counteragent>`.

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
- ``Status`` — статус контрагента. Принимает значения из перечисления :doc:`CounteragentStatus`.
- ``EventTimestampTicks`` — время последнего изменения статуса контрагента. Возвращается целое число тиков, прошедших с момента времени 00:00:00 01.01.0001.
- ``LastEventComment`` — текст сообщения из последнего взаимодействия с контрагентом.
- ``MessageFromCounteragent`` — текст сообщения, полученного от контрагента.
- ``MessageToCounteragent`` — текст сообщения, отправленнонго контрагенту.
- ``InvitationDocumentId`` — идентификатор документа, отправленного вместе с приглашением. Представлен структурой :doc:`DocumentId`.
- ``CounteragentGroupId`` — идентификатор группы, в которую добавлен контрагент.

----

.. rubric:: См. также

*Структура используется:*
	- в структуре :doc:`BoxCounteragentEvent <BoxCounteragentEventList>`