Content_v2
===========

.. code-block:: protobuf

        message Content_v2 {
            optional bytes Content = 1;
            optional string NameOnShelf = 2;
            optional string PatchedContentId = 3;
        }
        

Структура, описывающая данные (содержимое документов, файлов), либо как массив байтов, либо как ссылку в Диадоке.

-  *Content* - данные, как массив байтов.

-  *NameOnShelf* - Имя файла на полке. Подробнее в описании метода :doc:`../http/ShelfUpload`.

-  *PatchedContentId* - Идентификатор документа "подготовленного к отправке" методом :doc:`../http/PrepareDocumentsToSign`.