AutosignReceiptsResult
======================

.. code-block:: protobuf

            message AutosignReceiptsResult {
                required int64 SignedReceiptsCount = 1;
                required string NextBatchKey = 2;
            }


- *SignedReceiptsCount* - Количество подписанных уведомлений.
- *NextBatchKey* - Идентификатор следующей пачки уведомлений для подписания.
