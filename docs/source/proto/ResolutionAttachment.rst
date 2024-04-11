ResolutionAttachment
====================

Структура ``ResolutionAttachment`` содержит информацию о согласовании.

.. code-block:: protobuf

    message ResolutionAttachment {
        required string InitialDocumentId  = 1;
        required ResolutionType ResolutionType = 2;
        optional string Comment = 3;
        repeated string Labels = 4;
    }

- ``InitialDocumentId`` — идентификатор согласуемого документа
- ``ResolutionType`` — тип действия по согласованию, принимает значения из перечисления :doc:`ResolutionType`.
- ``Comment`` — комментарий к согласованию или отказу от согласования. Длина не должна превышать 5000 символов.
- ``Labels`` — :doc:`метки <../proto/Labels>` согласования или отказа от согласования.

----

.. rubric:: См. также

*Структура используется:*
	- в структуре :doc:`MessagePatchToPost`