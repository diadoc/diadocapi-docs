ResolutionRequestDenialCancellationAttachment
=============================================

Структура ``ResolutionRequestDenialCancellationAttachment`` содержит информацию об отмене отказа от запроса подписи к документу.

.. code-block:: protobuf

    message ResolutionRequestDenialCancellationAttachment {
        required string InitialResolutionRequestDenialId = 1;
    }

- ``InitialResolutionRequestDenialId`` — идентификатор отменяемого отказа от запроса подписи к документу.

----

.. rubric:: См. также

*Структура используется:*
	- в структуре :doc:`MessagePatchToPost`