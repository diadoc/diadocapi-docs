BoxCounteragentEventList
========================

Структура ``BoxCounteragentEventList`` представляет собой список событий по изменению отношений с :doc:`контрагентами <../entities/counteragent>`.

.. code-block:: protobuf

   message BoxCounteragentEventList {
        repeated BoxCounteragentEvent Events = 1;
        optional int32 TotalCount = 2;
        required TotalCountType TotalCountType = 3;
    }

    message BoxCounteragentEvent {
        required string EventId = 1;
        optional CounteragentInfo Counteragent = 2;
        optional string IndexKey = 3;
        repeated CounteragentEventType EventTypes = 4;
    }

    enum CounteragentEventType
    {
        UnknownCounteragentEventType = 0;
        IInvitedCounteragent = 1;
        CounteragentInvitedMe = 2;
        CounteragentAcceptedInvitation = 3;
        IAcceptedInvitation = 4;
        IWithdrewInvitation = 5;
        CounteragentWithdrewInvitation = 6;
        IRejectedInvitation = 7;
        CounteragentRejectedInvitation = 8;
        IBrokeUpWithCounteragent = 9;
        CounteragentBrokeUpWithMe = 10;
        IForgotCounteragent = 11;
        CounteragentForgotMe = 12;
        IMadeCounteragent = 13;
        CounteragentMadeMe = 14;
    }

- ``Events`` — список событий по изменению отношений с контрагентами. Каждое событие представлено структурой ``BoxCounteragentEvent`` с полями:

	- ``EventId`` — идентификатор события.
	- ``Counteragent`` — информация о контрагенте, представленная структурой :doc:`../proto/CounteragentInfo`.
	- ``IndexKey`` — ключ события, который можно передавать в качестве параметра ``afterIndexKey`` для итерирования по отфильтрованному списку.
	- ``EventTypes`` — тип события, произошедшего с контрагентом. Принимает значение из перечисления ``CounteragentEventType``:

		- ``UnknownCounteragentEventType`` — событие не определено;
		- ``IInvitedCounteragent`` — я отправил приглашение контрагенту;
		- ``CounteragentInvitedMe`` — контрагент отправил мне приглашение;
		- ``CounteragentAcceptedInvitation`` — контрагент принял мое приглашение;
		- ``IAcceptedInvitation`` — я принял приглашение контрагента;
		- ``IWithdrewInvitation`` — я отменил свое приглашение;
		- ``CounteragentWithdrewInvitation`` — контрагент отменил свое приглашение;
		- ``IRejectedInvitation`` — я отклонил приглашеие контрагента;
		- ``CounteragentRejectedInvitation`` — контрагент отклонил мое приглашение;
		- ``IBrokeUpWithCounteragent`` — я разорвал отношения с контрагентом;
		- ``CounteragentBrokeUpWithMe`` — контрагент разорвал отношения со мной;
		- ``IForgotCounteragent`` — отношения с конрагентом разорваны завершенным документооборотом или через настройку роуминга;
		- ``CounteragentForgotMe`` — отношения с конрагентом разорваны завершенным документооборотом или через настройку роуминга;
		- ``IMadeCounteragent`` — отношения с конрагентом установлены завершенным документооборотом или через настройку роуминга;
		- ``CounteragentMadeMe`` — отношения с конрагентом установлены завершенным документооборотом или через настройку роуминга.

- ``TotalCount`` — количество событий, удовлетворяющих запросу.
- ``TotalCountType`` — параметр, указывающий, является ли значение ``TotalCount`` точным или подсчет был ограничен максимальным количеством событий в ответе. Принимает значения из перечисления :doc:`../proto/TotalCountType`.

----

.. rubric:: См. также

*Структура используется:*
	- в теле ответа метода :doc:`../http/GetCounteragentEvents`

*Определение:*
	- :doc:`../entities/counteragent`

*Инструкции:*
	- :doc:`../instructions/counteragentevents`