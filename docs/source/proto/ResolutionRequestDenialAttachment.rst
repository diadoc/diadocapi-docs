ResolutionRequestDenialAttachment
=================================

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

----

.. rubric:: См. также

*Структура используется:*
	- в структуре :doc:`MessagePatchToPost`