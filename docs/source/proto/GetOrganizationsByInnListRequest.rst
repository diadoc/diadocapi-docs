GetOrganizationsByInnListRequest
================================

.. code-block:: protobuf

    message GetOrganizationsByInnListRequest {
        repeated string InnList = 1;
    }

    message OrganizationWithCounteragentStatus {
        required Organization Organization = 1;
        optional CounteragentStatus CounteragentStatus = 2 [default = UnknownCounteragentStatus];
        optional sfixed64 LastEventTimestampTicks = 3;
       	optional string MessageFromCounteragent = 4;
    	optional string MessageToCounteragent = 5;
        optional DocumentId InvitationDocumentId = 6;
    }

    message GetOrganizationsByInnListResponse {
        repeated OrganizationWithCounteragentStatus Organizations = 1;
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

Структура данных *GetOrganizationsByInnListRequest* содержит список ИНН организаций, который передается в тело запроса метода :doc:`../http/GetOrganizationsByInnList`:

-  *InnList* - ИНН организации

Структура данных *GetOrganizationsByInnListResponse* содержит список организаций, найденных по списку ИНН методом :doc:`../http/GetOrganizationsByInnList`:

-  :doc:`Organization` - содержит информацию об одной организации в Диадоке,

-  *CounteragentStatus* - статус контрагента для данной организации

-  *LastEventTimestampTicks* - :doc:`метка времени <Timestamp>` последнего события из истории взаимодействия с данным контрагентом

-  *MessageFromCounteragent* - сообщение пришедшее от контрагента вместе с приглашением

-  *MessageToCounteragent* - сообщение отправленное контрагенту вместе с приглашением

-  *InvitationDocumentId* - :doc:`DocumentId` идентификатор документа пришедший вместе с приглашением