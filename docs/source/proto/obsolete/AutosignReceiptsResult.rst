AutoSignReceiptsResult
======================

.. warning::
	Структура используется в устаревшем методе :doc:`../../http/obsolete/AutoSignReceiptsResult`.

Структура ``AutoSignReceiptsResult`` представляет собой состояние задачи на подписание извещений о получении ``InvoiceReceipt``.

.. code-block:: protobuf

            message AutoSignReceiptsResult {
                required int64 SignedReceiptsCount = 1;
                required string NextBatchKey = 2;
            }


- ``SignedReceiptsCount`` — количество подписанных извещений.
- ``NextBatchKey`` — идентификатор следующей пачки извещений для подписания.


----

.. rubric:: См. также

*Структура используется:*
	- в теле ответа устаревшего метода :doc:`../../http/obsolete/AutoSignReceiptsResult`