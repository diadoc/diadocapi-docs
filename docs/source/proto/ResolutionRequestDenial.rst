ResolutionRequestDenial
=======================

.. code-block:: protobuf

    message ResolutionRequestDenialInfo {
        required string Author = 1;
        optional string InitialRequestId = 2;
    }

    message ResolutionRequestDenialAttachment {
        required string InitialResolutionRequestId = 1;
        optional string Comment = 2;
    }

    message ResolutionRequestDenialCancellationAttachment {
        required string InitialResolutionRequestDenialId = 1;
    }
        

Структура данных ResolutionRequestDenialInfo содержит информацию об отказе от запроса подписи к документу.

-  Author - ФИО отказавшего сотрудника.

-  InitialRequestId - идентификатор запроса, по которому было отказано.

Структура данных ResolutionRequestDenialAttachment содержит информацию об отказе от запроса подписи к документу в методе :doc:`../http/PostMessagePatch`.

-  InitialResolutionRequestId - идентификатор запроса на подпись, для которого формируется отказ.

-  Comment - комментарий к отказу от запроса подписи к документу.

Структура данных ResolutionRequestDenialCancellationAttachment содержит информацию об отмене отказа от запроса подписи к документу в методе :doc:`../http/PostMessagePatch`.

-  InitialResolutionRequestDenialId - идентификатор отменяемого отказа от запроса подписи к документу.