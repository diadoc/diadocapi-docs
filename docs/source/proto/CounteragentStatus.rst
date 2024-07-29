CounteragentStatus
==================

Перечисление ``CounteragentStatus`` представляет собой статус :doc:`контрагента <../entities/counteragent>`.

.. code-block:: protobuf

    enum CounteragentStatus {
        UnknownCounteragentStatus = 0;
        IsMyCounteragent = 1;
        InvitesMe = 2;
        IsInvitedByMe = 3;
        RejectsMe = 5;
        IsRejectedByMe = 6;
        NotInCounteragentList = 7;
    }

- ``UnknownCounteragentStatus`` — неизвестный статус. Возвращается, если клиент использует устаревшую версию SDK и не может интерпретировать статус контрагента, переданный сервером.
- ``IsMyCounteragent`` — отношение партнерства установлено и действует.
- ``InvitesMe`` — контрагент прислал запрос на установление отношения партнерства.
- ``IsInvitedByMe`` — в адрес контрагента был отправлен запрос на установление отношения партнерства.
- ``RejectsMe`` — контрагент разорвал отношение партнерства или отклонил запрос на установление отношения партнерства.
- ``IsRejectedByMe`` — текущая организация разорвала отношение партнерства или отклонила запрос на установление отношения партнерства.
- ``NotInCounteragentList`` — организации нет в списке контрагентов. Методы :doc:`../http/GetCounteragent` и :doc:`../http/GetCounteragents` не возвращают этот статус в структуре :doc:`Counteragent`.

----

.. rubric:: См. также

*Перечисление используется:*
	- в структуре :doc:`Counteragent`
	- в структуре :doc:`CounteragentInfo`