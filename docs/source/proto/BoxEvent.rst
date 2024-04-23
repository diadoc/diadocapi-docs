BoxEvent
========

Структура ``BoxEvent`` представляет собой событие в :doc:`ящике<../entities/box>`.

.. code-block:: protobuf

    message BoxEvent {
        required string EventId = 1;
        optional Message Message = 2;
        optional MessagePatch Patch = 3;
        optional string IndexKey = 4;
    }

- ``EventId`` — идентификатор события.
- ``Message`` — новое сообщение или черновик, представленный структурой :doc:`Message`. Не может быть заполнено одновременно с ``Patch``.
- ``Patch`` — новое дополнение к уже существующему в ящике сообщению или черновику, представленное структурой :doc:`MessagePatch`.
- ``IndexKey`` — ключ события, который можно передавать в метод :doc:`../http/GetNewEvents` в качестве параметра ``afterIndexKey`` для итерирования по отфильтрованному списку.

----

.. rubric:: См. также

*Структура используется:*
	- в структуре :doc:`BoxEventList`
	- в теле ответа метода :doc:`../http/GetEvent`
	- в теле ответа метода :doc:`../http/GetLastEvent`

*Руководства:*
	- :doc:`../features/docflow`