Attachment
==========

.. code-block:: protobuf

   message Attachment
   {
       optional Entity Entity = 1;
       optional string AttachmentFilename = 2;
       optional string DisplayFilename = 3;
   }

Структура представляет базовую информацию о документе.

-  :doc:`Entity` - информация о содержимом файла.
-  *AttachmentFilename* - имя файла.
-  *DisplayFilename* - название документа, пригодное для отображения в интерфейсе. Например, для счёта-фактуры оно будет иметь вид "Счет-фактура №1 от 01.02.03".
