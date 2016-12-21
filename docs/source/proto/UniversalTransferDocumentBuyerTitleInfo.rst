UniversalTransferDocumentBuyerTitleInfo 
=======================================

.. code-block:: protobuf

    message UniversalTransferDocumentBuyerTitleInfo {
        required string DocumentCreator = 1; // НаимЭконСубСост - Наименование экономического субъекта - составителя файла обмена информации покупателя
        optional string DocumentCreatorBase = 2; // ОснДоверОргСост - Основание, по которому экономический субъект является составителем файла обмена информации покупателя
        optional string OperationCode = 3; // ВидОперации - ВидОперации
        required string OperationContent = 4; // СодОпер - Содержание операции
        optional string AcceptanceDate = 5; // ДатаПрин - Дата принятия товаров (результатов выполненных работ), имущественных прав (подтверждения факта оказания услуг)
        optional Employee Employee = 6; // РабОргПок - работник организации покупателя
        optional OtherIssuer OtherIssuer = 7; // ИнЛицо - Иное Лицо
        optional AdditionalInfoId AdditionalInfoId = 8; // ИнфПолФХЖ4
        repeated Signers.ExtendedSigner Signers = 9; // Подписант
    }
    
Структура данных *UniversalTransferDocumentBuyerTitleInfo* представляет исходные данные для формирования файлов в XML-формате при помощи метода :doc:`../http/GenerateUniversalTransferDocumentXmlForBuyer`. При заполнении структуры *UniversalTransferDocumentBuyerTitleInfo* нужно иметь в виду:

-  Реквизиты подписанта счета-фактуры UniversalTransferDocumentBuyerTitleInfo.Signers заполняются в виде структуры данных :doc:`ExtendedSigner`.

-  Даты документов должны указываться в формате ДД.ММ.ГГГГ.

-  Информация о работнике покупателя представляется в виде структуры :doc:`Employee <UniversalTransferDocumentSellerTitleInfo>`.

-  Информация о ином лице, принявшем товар, представляется в виде структуры :doc:`OtherIssuer <UniversalTransferDocumentSellerTitleInfo>`.

-  Сведения информационного поля о факте хозяйственной жизни представляется в виде структуры :doc:`AdditionalInfoId <UniversalTransferDocumentSellerTitleInfo>`.