Attachment
==========

Структура ``Attachment`` представляет собой базовую информацию о документе внутри сообщения.

.. code-block:: protobuf

    message Attachment
    {
        optional Entity Entity = 1;
        optional string AttachmentFilename = 2;
        optional string DisplayFilename = 3;
    }

- ``Entity`` — информация о содержимом документа, представленная структурой :doc:`Entity`.
- ``AttachmentFilename`` — имя файла документа при загрузке в Диадок.
- ``DisplayFilename`` — название документа; используется для отображения в веб-интерфейсе. Например, для счета-фактуры название будет иметь вид «Счет-фактура №1 от 01.02.03». Используйте только символы, разрешенные в HTML: все недопустимые символы будут преобразованы.


----

.. rubric:: См. также

*Структура используется:*
	- в структуре :doc:`SignedAttachment`
	- в структуре :doc:`SignedAttachmentV3`