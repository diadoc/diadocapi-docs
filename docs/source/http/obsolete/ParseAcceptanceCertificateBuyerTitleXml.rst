ParseAcceptanceCertificateBuyerTitleXml
========================================

.. warning::
	Метод устарел. Для парсинга документов используйте метод :doc:`../ParseTitleXml`.

.. http:post:: /ParseAcceptanceCertificateBuyerTitleXml

    :query documentVersion: версия документа

    :statuscode 200: операция успешно завершена
    :statuscode 400: данные в запросе имеют неверный формат или отсутствуют обязательные параметры
    :statuscode 405: используется неподходящий HTTP-метод
    :statuscode 500: при обработке запроса возникла непредвиденная ошибка

    Если *documentVersion* равен ``rezru_05_01_02``:

    - в теле запроса должен содержаться XML-файл акта, титул заказчика, удовлетворяющий :download:`XSD-схеме (DP_REZRUZAK_1_990_02_05_01_02.xsd) <../../xsd/DP_REZRUZAK_1_990_02_05_01_02.xsd>`;

    - в теле ответа содержится сериализованная структура :doc:`AcceptanceCertificate552BuyerTitleInfo <../../proto/obsolete/AcceptanceCertificate552Info>`, построенная на основании данных запроса;

    Если *documentVersion* не указан или равен ``act_05_01_02``:

    - в теле запроса должен содержаться XML-файл акта, титул заказчика, удовлетворяющий :download:`XSD-схеме (DP_ZAKTPRM_1_990_00_05_01_02.xsd) <../../xsd/DP_ZAKTPRM_1_990_00_05_01_02.xsd>`;

    - в теле ответа содержится сериализованная структура :doc:`AcceptanceCertificateBuyerTitleInfo <../../proto/obsolete/AcceptanceCertificateInfo>`, построенная на основании данных запроса;
