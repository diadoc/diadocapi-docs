ResolutionRequestDenial
=======================

На этой странице описаны следующие структуры:

.. contents:: :local:

.. _ResolutionRequestDenialInfo:

ResolutionRequestDenialInfo
---------------------------

Структура ``ResolutionRequestDenialInfo`` содержит информацию об отказе в запросе подписи к документу.

.. code-block:: protobuf

    message ResolutionRequestDenialInfo {
        required string Author = 1;
        optional string InitialRequestId = 2;
    }

- ``Author`` — ФИО отказавшего сотрудника.
- ``InitialRequestId`` — идентификатор запроса, по которому было отказано.


.. _ResolutionRequestDenialAttachment:

ResolutionRequestDenialAttachment
---------------------------------

Структура ``ResolutionRequestDenialAttachment`` содержит информацию о действиях, отменяющих отказы от запросов подписей к документу.

.. code-block:: protobuf

    message ResolutionRequestDenialAttachment {
        required string InitialResolutionRequestId = 1;
        optional string Comment = 2;
        repeated string Labels = 3;
    }

- ``InitialResolutionRequestId`` — идентификатор запроса на подпись, для которого формируется отказ.
- ``Comment`` — комментарий к отказу от запроса подписи к документу. Длина не более 500 символов.
- ``Labels`` — :doc:`метки <../proto/Labels>` отказа от запроса подписи.

.. _ResolutionRequestDenialCancellationAttachment:

ResolutionRequestDenialCancellationAttachment
---------------------------------------------

Структура ``ResolutionRequestDenialCancellationAttachment`` содержит информацию об отмене отказа от запроса подписи к документу.

.. code-block:: protobuf

    message ResolutionRequestDenialCancellationAttachment {
        required string InitialResolutionRequestDenialId = 1;
    }

- ``InitialResolutionRequestDenialId`` — идентификатор отменяемого отказа от запроса подписи к документу.