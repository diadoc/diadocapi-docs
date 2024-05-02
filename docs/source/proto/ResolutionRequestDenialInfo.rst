ResolutionRequestDenialInfo
===========================

Структура ``ResolutionRequestDenialInfo`` содержит информацию об отказе в запросе подписи к документу.

.. code-block:: protobuf

    message ResolutionRequestDenialInfo {
        required string Author = 1;
        optional string InitialRequestId = 2;
    }

- ``Author`` — ФИО отказавшего сотрудника.
- ``InitialRequestId`` — идентификатор запроса, по которому было отказано.

----

.. rubric:: См. также

*Структура используется:*
	- в структуре :doc:`Entity message`

