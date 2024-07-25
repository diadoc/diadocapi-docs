GetOrganizationsByInnListResponse
=================================

Структура ``GetOrganizationsByInnListResponse`` представляет собой список организаций, найденных по списку ИНН.

.. code-block:: protobuf

    message GetOrganizationsByInnListResponse {
        repeated OrganizationWithCounteragentStatus Organizations = 1;
    }

    message OrganizationWithCounteragentStatus {
        required Organization Organization = 1;
        optional CounteragentStatus CounteragentStatus = 2 [default = UnknownCounteragentStatus];
        optional sfixed64 LastEventTimestampTicks = 3;
        optional string MessageFromCounteragent = 4;
        optional string MessageToCounteragent = 5;
        optional DocumentId InvitationDocumentId = 6;
        optional string CounteragentGroupId = 7;
    }

    enum CounteragentStatus {
        UnknownCounteragentStatus = 0;
        IsMyCounteragent = 1;
        InvitesMe = 2;
        IsInvitedByMe = 3;
        RejectsMe = 5;
        IsRejectedByMe = 6;
        NotInCounteragentList = 7;
    }

- ``Organizations`` — список найденных организаций. Каждая организация представлена структурой ``OrganizationWithCounteragentStatus`` с полями:

	- ``Organization`` — информация об одной организации в Диадоке. Представлена структурой :doc:`Organization`.

	- ``CounteragentStatus`` — статус контрагента, принимает значения из перечисления ``CounteragentStatus``:

		- ``UnknownCounteragentStatus`` — неизвестный статус контрагента. Может выдаваться, если клиент использует устаревшую версию SDK и не может интерпретировать статус контрагента, переданный сервером.
		- ``IsMyCounteragent`` — отношение партнерства установлено и действует.
		- ``InvitesMe`` — контрагент прислал запрос на установление отношения партнерства.
		- ``IsInvitedByMe`` — организация отправила контрагенту запрос на установление отношения партнерства.
		- ``RejectsMe`` — контрагент разорвал отношения партнерства или отклонил запрос на установление отношения партнерства.
		- ``IsRejectedByMe`` — организация разорвала отношения партнерства или отклонила запрос на установление отношения партнерства.
		- ``NotInCounteragentList`` — организации нет в списке контрагентов.

	- ``LastEventTimestampTicks`` — :doc:`время <Timestamp>` последнего взаимодействия с контрагентом.

	- ``MessageFromCounteragent`` — сообщение, пришедшее от контрагента вместе с приглашением.

	- ``MessageToCounteragent`` — сообщение, отправленное контрагенту вместе с приглашением.

	- ``InvitationDocumentId`` — идентификатор документа, пришедшего вместе с приглашением. Представлен структурой :doc:`DocumentId`.

	- ``CounteragentGroupId`` — идентификатор группы, в которую добавлен контрагент. Возвращается, если статус контрагента ``CounteragentStatus = IsMyCounteragent``. Инструкция по работе с группами контрагентов приведена  на странице :doc:`../instructions/counteragentgroups`.

----

.. rubric:: См. также

*Структура используется:*
	- в теле ответа метода :doc:`../http/GetOrganizationsByInnList`