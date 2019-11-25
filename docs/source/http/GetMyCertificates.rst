GetMyCertificates
=================

Метод возвращает информацию о сертификатах, привязанных к сотруднику.

.. http:get:: /GetMyCertificates

    :query boxId: идентификатор ящика сотрудника

    :reqheader Authorization: необходимые данные для :doc:`авторизации <../Authorization>`

    :statuscode 200: операция успешно завершена
    :statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization``, или в этом заголовке содержатся некорректные авторизационные данные
    :statuscode 405: используется неподходящий HTTP-метод
    :statuscode 500: при обработке запроса возникла непредвиденная ошибка

**Тело ответа:** структура CertificateList

.. code-block:: protobuf

    message CertificateList {
        repeated CertificateInfoV2 Certificates = 1;
    }

    message CertificateInfoV2 {
        required string Thumbprint = 1;
        required CertificateType Type = 2;
        optional sfixed64 ValidFrom = 3;
        optional sfixed64 ValidTo = 4;
        optional sfixed64 PrivateKeyValidFrom = 5;
        optional sfixed64 PrivateKeyValidTo = 6;
        optional string OrganizationName = 7;
        optional string Inn = 8;
        optional string UserFirstName = 9;
        optional string UserMiddleName = 10;
        optional string UserLastName = 11;
        optional string UserShortName = 12;
        optional bool IsDefault = 13;
    }

    enum CertificateType {
        Unknown = 0;
        Token = 1;
        Dss = 2;
        KonturCertificate = 3;
    }

Структура *CertificateInfoV2* содержит набор полей из публичной части сертификата сотрудника, таких как отпечаток, тип сертификата (железный носитель, Контур.Сертификат или DSS-сертификат), информация о субъектах.

Параметр *IsDefault* означает, выбран ли сертификат для работы по умолчанию в организации сотрудника. Например, от этого зависит автоматическое подписание извещений о получений в веб-интерфейсе Диадока.
