Content_v3
==========

.. code-block:: protobuf

        message Content_v3 {
            optional bytes Content = 1;
            optional string NameOnShelf = 2;
            optional DocumentId EntityId = 3;
            optional string PatchedContentId = 4;
        }
        

Структура описывает данные (содержимое документа, файла) либо как массив байтов, либо как ссылку на загруженный файл в Диадоке.

-  *Content* - данные как массив байтов

-  *NameOnShelf* - имя файла на полке (подробнее в описании метода :doc:`../http/ShelfUpload`)

-  :doc:`EntityId <DocumentId>` - идентификатор сущности в Диадоке

-  *PatchedContentId* - Идентификатор документа, "подготовленного к отправке" методом :doc:`../http/PrepareDocumentsToSign`.

Должно быть заполнено ровно одно из полей *Content*, *NameOnShelf*, *EntityId*, *PatchedContentId*.