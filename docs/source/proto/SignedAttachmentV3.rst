SignedAttachmentV3
==================

.. warning:: Эта версия контракта — экспериментальная и может измениться.

.. code-block:: protobuf

   message SignedAttachmentV3
   {
        required Attachment Attachment = 1;
        optional SignatureV3 Signature = 2;
        optional Entity Comment = 3;
        required string ContentTypeId = 4;
   }

Структура представляет базовую информацию о документе и его подписи.

-  :doc:`Attachment` - данные файла документа.
-  :doc:`SignatureV3` - подпись под файлом.
-  :doc:`Comment <Entity>` - комментарий к файлу.
-  *ContentTypeId* - уникальный идентификатор контента документа. ContentTypeId будет единым для документов с одинаковой структурой и одинаковыми правилами обработки. Идентификатор будет свой для каждого типа документа, титула и служебного документа. Например, УПД 820 формата с функцией СЧФДОП будет иметь ContentTypeId=utd820_schfdop_orig_t1_05_01_01 для первого титула и utd820_schfdop_t2_05_01_01 для второго титула, а для отказа в подписи в формате уведомления об уточнении ContentTypeId = signature_rejection_02
