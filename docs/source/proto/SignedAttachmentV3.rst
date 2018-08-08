SignedAttachmentV3
==================

.. warning:: Эта версия контракта — экспериментальная и может измениться.

.. code-block:: protobuf

   message SignedAttachment
   {
        required Attachment Attachment = 1;
        optional SignatureV3 Signature = 2;
        optional Entity Comment = 3;
   }

Структура представляет базовую информацию о документе и его подписи.

-  :doc:`Attachment` - данные файла документа.
-  :doc:`SignatureV3` - подпись под файлом.
-  :doc:`Comment <Entity>` - комментарий к файлу.
