ParseAcceptanceCertificateSellerTitleXml
========================================

.. warning::
	Метод устарел. Для парсинга документов используйте метод :doc:`../ParseTitleXml`.

.. http:post:: /ParseAcceptanceCertificateSellerTitleXml

    :query documentVersion: версия документа

    :statuscode 200: операция успешно завершена
    :statuscode 400: данные в запросе имеют неверный формат или отсутствуют обязательные параметры
    :statuscode 405: используется неподходящий HTTP-метод
    :statuscode 500: при обработке запроса возникла непредвиденная ошибка

    Если *documentVersion* равен ``rezru_05_01_02``:

    - в теле запроса должен содержаться XML-файл акта, титул исполнителя, удовлетворяющий :download:`XSD-схеме (DP_REZRUISP_1_990_01_05_01_02.xsd) <../../xsd/DP_REZRUISP_1_990_01_05_01_02.xsd>`.

    - в теле ответа содержится сериализованная структура :doc:`AcceptanceCertificate552SellerTitleInfo <../../proto/obsolete/AcceptanceCertificate552Info>`, построенная на основании данных запроса;

    Если *documentVersion* не указан или равен ``act_05_01_02``:

    - в теле запроса должен содержаться XML-файл акта, титул исполнителя, удовлетворяющий :download:`XSD-схеме (DP_IAKTPRM_1_987_00_05_01_02.xsd) <../../xsd/DP_IAKTPRM_1_987_00_05_01_02.xsd>`.

    - в теле ответа содержится сериализованная структура :doc:`AcceptanceCertificateSellerTitleInfo <../../proto/obsolete/AcceptanceCertificateInfo>`, построенная на основании данных запроса;
