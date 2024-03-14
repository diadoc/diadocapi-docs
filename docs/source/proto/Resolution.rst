Resolution
==========

На этой странице описаны следующие структуры:

.. contents:: :local:

.. _ResolutionInfo:

ResolutionInfo
--------------

Структура ``ResolutionInfo`` содержит информацию о состоянии согласования.

.. code-block:: protobuf

    message ResolutionInfo {
        optional ResolutionType ResolutionType = 1 [default = UnknownResolutionType];
        required string Author = 2;
        optional string InitialRequestId = 3;
    }

- ``ResolutionType`` — тип действия по согласованию, принимает значения из перечисления :ref:`ResolutionType`.
- ``Author`` — ФИО пользователя, согласовавшего или отказавшего в согласовании.
- ``InitialRequestId`` — идентификатор запроса, в ответ на который сформировано согласование.

.. _ResolutionType:

ResolutionType
--------------

Перечисление ``ResolutionType`` представляет собой тип действия по согласованию.

.. code-block:: protobuf

    enum ResolutionType {
        UndefinedResolutionType = 0;
        Approve = 1;
        Disapprove = 2;
        UnknownResolutionType = 3;
    }

- ``UndefinedResolutionType`` — отменить последнее согласование текущего пользователя.
- ``Approve`` — согласовать документ.
- ``Disapprove`` — отказать в согласовании документа.
- ``UnknownResolutionType`` — неизвестное состояние. Возвращается в случае, если клиент использует устаревшую версию SDK и не может интерпретировать состояние согласования, переданное сервером.


ResolutionAttachment
--------------------

Структура ``ResolutionAttachment`` содержит информацию о согласовании.

.. code-block:: protobuf

    message ResolutionAttachment {
        required string InitialDocumentId  = 1;
        required ResolutionType ResolutionType = 2;
        optional string Comment = 3;
        repeated string Labels = 4;
    }

- ``InitialDocumentId`` — идентификатор согласуемого документа
- ``ResolutionType`` — тип действия по согласованию, принимает значения из перечисления :ref:`ResolutionType`.
- ``Comment`` — комментарий к согласованию или отказу от согласования. Длина не должна превышать 5000 символов.
- ``Labels`` — :doc:`метки <../proto/Labels>` согласования или отказа от согласования.