ResolutionStatus
================

.. code-block:: protobuf

    message ResolutionStatus {
        required ResolutionStatusType Type = 1;
        optional ResolutionTarget Target = 2;
        required string AuthorUserId = 3;
        required string AuthorFIO = 4;
    }

    enum ResolutionStatusType {
        None = 0;
        Approved = 1;
        Disapproved = 2;
        ApprovementRequested = 3;
        SignatureRequested = 4;
        SignatureDenied = 5;
    }

    message ResolutionTarget {
        optional string Department = 1;
        optional string DepartmentId = 2;
        optional string User = 3;
        optional string UserId = 4;
    }
        

Структура ResolutionStatus содержит информацию, о текущем статусе согласования документа. Используется как часть структуры :doc:`Document`.

ResolutionStatusType - тип статуса согласования:

-  None - документ не согласовывался

-  Approved - Согласован

-  Disapproved - В согласовании отказано

-  ApprovementRequested - Запрошено согласование

-  SignatureRequested - Запрошена подпись

-  SignatureDenied - В подписи отказано

Структура ResolutionTarget заполняется только при запросе согласования или подписи, и описывает получателя запроса. Получателем запроса на согласование или подпись может быть:

-  либо в подразделение, тогда заполняются идентификатор и название подразделения (поля DepartmentId и Department)

-  либо конкретный пользователь, тогда заполняются идентификатор и ФИО пользователя (поля UserId и User)

Поля ResolutionStatus.AuthorUserId и ResolutionStatus.AuthorFIO - содержат идентификатор и ФИО пользователя, который совершил действие, описываемое данным статусом (т.е согласовал/отказал или передал на согласование/подпись).