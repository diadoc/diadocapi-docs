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

Примеры ответов
---------------

::

    HTTP/1.1 200 OK
    Content-Type: application/json; charset=utf-8

    {
        "Certificates": []
    }

::

    HTTP/1.1 200 OK
    Content-Type: application/json; charset=utf-8

    {
        "Certificates": [
            {
                "Thumbprint": "6B************************************D7",
                "Type": "Dss",
                "ValidFrom": 637033581700000000,
                "ValidTo": 637428429700000000,
                "PrivateKeyValidFrom": 637033581700000000,
                "PrivateKeyValidTo": 637428429700000000,
                "OrganizationName": "ООО Васильки",
                "Inn": "60*******43",
                "UserFirstName": "Петр",
                "UserMiddleName": "Алексеевич",
                "UserLastName": "Иванов",
                "UserShortName": "Иванов П. А.",
                "IsDefault": false
            },
            {
                "Thumbprint": "BA************************************81",
                "Type": "Token",
                "ValidFrom": 636965170070000000,
                "ValidTo": 637360882070000000,
                "PrivateKeyValidFrom": 636965170060000000,
                "PrivateKeyValidTo": 637360882060000000,
                "OrganizationName": "ООО Ромашки",
                "Inn": "62*******14",
                "UserFirstName": "Петр",
                "UserMiddleName": "Алексеевич",
                "UserLastName": "Иванов",
                "UserShortName": "Иванов П. А.",
                "IsDefault": true
            }
        ]
    }
