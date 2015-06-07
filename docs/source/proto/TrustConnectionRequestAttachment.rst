TrustConnectionRequestAttachment
================================

.. code-block:: protobuf

    message TrustConnectionRequestAttachment {
        required SignedContent SignedContent = 1;
        required string FileName = 2;
        optional string Comment = 3;
        optional string CustomDocumentId = 4;
        repeated CustomDataItem CustomData = 5;
    }
        

Структура данных TrustConnectionRequestAttachment представляет запрос на инициацию канала обмена документами через Диадок в отправляемом сообщении :doc:`MessageToPost`:

-  SignedContent - содержимое файла запроса вместе с ЭЦП под ним в виде структуры :doc:`SignedContent`.

-  FileName - имя файла отправляемого запроса.

-  Comment - необязательный текстовый комментарий к запросу.

-  CustomDocumentId - необязательный идентификатор документа во внешней системе, уникальный в рамках структуры MessageToPost; используется для выстраивания связей между документами внутри отправляемого сообщения. В дальнейшем его можно получить через Document.CustomDocumentId.

-  CustomData - список пар вида "ключ-значение", содержащих произвольные данные по документу. Каждая пара задается структурой :doc:`CustomDataItem <CustomDataItem>`.