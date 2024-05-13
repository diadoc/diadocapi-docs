ResolutionRequestCancellationAttachment
=======================================

Структура ``ResolutionRequestCancellationAttachment`` содержит информацию для отправки отмены запроса на согласование документа.

.. code-block:: protobuf

    message ResolutionRequestCancellationAttachment {
        required string InitialResolutionRequestId = 1;
        optional string Comment = 2;
        repeated string Labels = 3;
    }

- ``InitialResolutionRequestId`` — идентификатор отменяемого запроса на согласование.
- ``Comment`` — комментарий к отмене запроса на согласование. Длина не должна превышать 256 символов.
- ``Labels`` — :doc:`метки <../entities/label>` отмены запроса на согласование.

----

.. rubric:: См. также

*Структура используется:*
	- в структуре :doc:`MessagePatchToPost`