AutoSignReceiptsResult
======================

.. warning::
	Структура используется устаревшим методом :doc:`../../http/obsolete/AutoSignReceiptsResult`.

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
	- в теле ответа метода :doc:`../../http/obsolete/AutoSignReceiptsResult`