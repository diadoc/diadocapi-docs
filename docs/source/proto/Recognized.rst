Recognized
==========

.. code-block:: protobuf

    message Recognized {
        required string RecognitionId = 1;
        optional string ErrorMessage = 2;
        optional string FileName = 3;
        optional RecognizedDocumentType DocumentType = 4 [default = UnknownRecognizedDocumentType];
        optional bytes Content = 5;
        optional RecognizedInvoice Invoice = 6;
    }

    enum RecognizedDocumentType {
        UnknownRecognizedDocumentType = -1;
        Invoice = 1;
    }

    message RecognizedInvoice {
        required string MetadataJson = 1;
        optional string ValidationErrorMessage = 2;
    }
        

Структура данных Recognized представляет статус задачи на распознавание либо результат распознавания:

-  RecognitionId - уникальный идентификатор задачи на распознавание.

-  ErrorMessage - текст ошибки в случае неуспешного распознавания.

-  FileName - имя файла результата (может отличаться от имени файла, переданного в метод :doc:`../http/Recognize`). Заполняется только в случае успешного распознавания.

-  DocumentType - тип распознанного документа: возможные варианты:

   -  UnknownRecognizedDocumentType (неизвестный тип документа; может выдаваться лишь в случае, когда клиент использует устаревшую версию SDK и не может интерпретировать тип документа, переданный сервером),
   -  Invoice (счет-фактура).

-  Content - содержимое распознанного файла. Заполняется только в случае успешного распознавания. В случае счета-фактуры содержит XML-файл в формате,довлетворяющем требованиям ФНС и пригодном для отправки СФ в соответствии с порядком, утвержденным Минфином РФ.

-  Invoice - дополнительная информация для счета-фактуры. Заполняется только в случае успешного распознавания документа. Имеет смысл только для документов с типом DocumentType = Invoice. Поле Invoice.MetadataJson - метаданные счета-фактуры в формате JSON. Поле Invoice.ValidationErrorMessage - строка с текстом ошибки валидации XML-документа счета-фактуры по XSD-схеме.