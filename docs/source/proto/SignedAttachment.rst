SignedAttachment
================

.. code-block:: protobuf

   message SignedAttachment
   {
       optional Attachment Attachment = 1;
       optional Signature Signature = 2;
       optional Entity Comment = 3;
   }

Структура представляет базовую информацию о документе и его подписи.

-  :doc:`Attachment` - данные файла документа.
-  :doc:`Signature` - подпись под файлом.
-  :doc:`Comment <Entity>` - комментарий к файлу.
