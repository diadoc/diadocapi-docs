GetMyCertificates
=================

Метод ``GetMyCertificates`` возвращает информацию о :doc:`сертификатах <../entities/certificate>`, привязанных к сотруднику.

.. http:get:: /GetMyCertificates

	:queryparam boxId: идентификатор ящика сотрудника.

	:requestheader Authorization: данные, необходимые для :doc:`авторизации <../Authorization>`.

	:statuscode 200: операция успешно завершена.
	:statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization`` или в этом заголовке содержатся некорректные авторизационные данные.
	:statuscode 402: у организации с указанным идентификатором ``boxId`` закончилась подписка на API.
	:statuscode 405: используется неподходящий HTTP-метод.
	:statuscode 500: при обработке запроса возникла непредвиденная ошибка.

	:response Body: Тело ответа содержит список сертификатов, представленный структурой :doc:`CertificateList <../proto/CertificateInfoV2>`.

Примеры ответов
^^^^^^^^^^^^^^^

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
                "Thumbprint": "BA************************************81",
                "Type": "Token",
                "ValidFrom": 636965170070000000,
                "ValidTo": 637360882070000000,
                "PrivateKeyValidFrom": 636965170060000000,
                "PrivateKeyValidTo": 637360882060000000,
                "OrganizationName": "ООО Ромашки",
                "Inn": "62******14",
                "UserFirstName": "Петр",
                "UserMiddleName": "Алексеевич",
                "UserLastName": "Иванов",
                "UserShortName": "Иванов П. А.",
                "IsDefault": true,
                "SubjectType": "LegalEntity"
            },
                    {
                "Thumbprint": "D7************************************4D",
                "Type": "Token",
                "ValidFrom": 637913122540000000,
                "ValidTo": 638307960600000000,
                "PrivateKeyValidFrom": 637913122540000000,
                "PrivateKeyValidTo": 638307960600000000,
                "OrganizationName": "",
                "Inn": "66********02",
                "UserFirstName": "Петр",
                "UserMiddleName": "Алексеевич",
                "UserLastName": "Иванов",
                "UserShortName": "Иванов П. А.",
                "IsDefault": false,
                "SubjectType": "PhysicalPerson"
            }
        ]
    }