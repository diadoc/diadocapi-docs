AutosignReceiptsResult
===============

.. code-block:: protobuf

            message AutosignReceiptsResult {
                optional string NextBatchKey = 1;
                optional int32 SignedReceiptsCount = 1;
            }
            

*NextBatchKey* - Идентификатор следующей пачки уведомлений для подписания.
*SignedReceiptsCount* - Кол-во подписанных уведомлений.
