Resolution
==========

.. code-block:: protobuf

    message ResolutionInfo {
        optional ResolutionType ResolutionType = 1 [default = UnknownResolutionType];
        required string Author = 2; // ФИО согласователя
        optional string InitialRequestId = 3;
    }

    enum ResolutionType {
        Undefined = 0;
        Approve = 1;
        Disapprove = 2;
        UnknownResolutionType = 3;
    }

    message ResolutionAttachment {
        required string DocumentId = 1;
        required ResolutionType ResolutionType = 2;
        optional string Comment = 3;
    }
        

Структура данных ResolutionInfo содержит информацию о состоянии согласования.

-  ResolutionType - тип действия по согласованию.

   -  Undefined - отменить последнее согласование текущего пользователя.

   -  Approve - согласовать документ.

   -  Disapprove - отказать в согласовании документа.

   -  UnknownResolutionType - неизвестное состояние (может выдаваться лишь в случае, когда клиент использует устаревшую версию SDK и не может интерпретировать состояние согласования, переданное сервером).

-  Author - ФИО согласователя.

-  InitialRequestId - идентификатор запроса, в ответ на который сформировано согласование.

Структура данных ResolutionAttachment задает информацию о согласовании в методе :doc:`../http/PostMessagePatch`.

-  DocumentId - идентификатор согласуемого документа

-  ResolutionType - тип действия по согласованию

-  Comment - комментарий к согласованию (отказу от согласования).