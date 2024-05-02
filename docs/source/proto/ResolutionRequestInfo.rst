ResolutionRequestInfo
=====================

Структура ``ResolutionRequestInfo`` содержит информацию о состоянии запроса на согласование.

.. code-block:: protobuf

    message ResolutionRequestInfo {
        optional ResolutionRequestType Type = 1 [default = UnknownResolutionRequestType];
        required string Author = 2;
        optional ResolutionTarget Target = 3;
        optional string ResolvedWith = 4;
        repeated ResolutionAction Actions = 5;
    }

- ``Type`` — тип запроса на согласование, представленный структурой :doc:`ResolutionRequestType`.
- ``Author`` — ФИО инициатора запроса.
- ``Target`` — информация о том, кому направлен запрос, представленная структурой :doc:`ResolutionTarget`.
- ``ResolvedWith`` — идентификатор ответного действия: положительное или отрицательное согласование, отказ в запросе подписи.
- ``Actions`` — список действий, которые можно выполнить в рамках текущего запроса на согласование. Каждый элмент списка представлен структурой :doc:`ResolutionAction`.

----

.. rubric:: См. также

*Структура используется:*
	- в структуре :doc:`Entity message`
