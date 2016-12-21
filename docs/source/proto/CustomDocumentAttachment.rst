CustomDocumentAttachment
========================

.. code-block:: protobuf
    
    message CustomDocumentAttachment {
        required SignedContent SignedContent = 1;
        required string FileName = 2;
        optional string Comment = 3;
        repeated DocumentId InitialDocumentIds = 5;
        repeated DocumentId SubordinateDocumentIds = 6;
        optional string CustomDocumentId = 9;
        repeated CustomDataItem CustomData = 11;
        required string Type = 12;
    }