GetRoamingOperators
===================

Метод ``GetRoamingOperators`` возвращает список роуминговых операторов и их функции.

.. http:get:: /GetRoamingOperators

	:queryparam boxId: идентификатор :doc:`ящика <../entities/box>` организации.
	
	:requestheader Authorization: данные, необходимые для :doc:`авторизации <../Authorization>`.

	:statuscode 200: операция успешно завершена.
	:statuscode 400: данные в запросе имеют неверный формат или отсутствуют обязательные параметры.
	:statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization`` или в этом заголовке содержатся некорректные авторизационные данные.
	:statuscode 402: у организации с указанным идентификатором ``boxId`` закончилась подписка на API.
	:statuscode 405: используется неподходящий HTTP-метод.
	:statuscode 500: при обработке запроса возникла непредвиденная ошибка.

	:response Body: Тело ответа содержит список роуминговых операторов, представленных структурой :doc:`../proto/RoamingOperatorInformation`. Она содержит информацию о роуминговом операторе и о функциях, которые поддерживает оператор на момент вызова метода.

Метод возвращает информацию о функциях роумингового оператора:

- ``SupportsRevocation`` — аннулирование версии 1.01.
- ``EnableRevocationV2`` — аннулирование версии 1.02.
- ``SupportsAutoInvitation`` — автоматическая обработка приглашений или автороуминг. Чтобы установить отношения с контрагентом, пользователю достаточно отправить приглашение. Заявку на роуминг отправлять не нужно.
- ``SupportsPowerOfAttorney`` — поддержка работы с машиночитаемой доверенностью.
- ``SupportsReconciliationAct`` — получение акта сверки в формате, утвержденном приказом `№ ЕД-7-26/405@ <https://normativ.kontur.ru/document?moduleId=1&documentId=425482>`__.
- ``SupportsTorg2``— получение акта об установленном расхождении ТОРГ-2 в формате, утвержденном приказом `№ ММВ-7-15/423@ <https://normativ.kontur.ru/document?moduleId=1&documentId=348230>`__.
- ``SupportsPerformedWorkAcceptanceCertificate`` — получение акта о приемке выполненных работ КС-2 в формате, утвержденном приказом `№ ЕД-7-26/691 <https://normativ.kontur.ru/document?moduleId=1&documentId=431929>`__.
- ``SupportPowerOfAttorneyFiles`` — поддержка работы с машиночитаемой доверенностью в виде файла.
- ``SupportPowerOfAttorneyDelegationChain`` — поддержка работы с машиночитаемой доверенностью, выпущенной в порядке передоверия.

**Пример ответа метода:**

.. sourcecode:: js 

    {
        "RoamingOperators": [
            {
                "FnsId": "1fr",
                "Name": "Финтендер",
                "IsActive": true,
                "Features": [
                    {
                        "Name": "SupportsAutoInvitation",
                        "Description": "Автоматическая обработка приглашений"
                    }
                ]
            },
            {
                "FnsId": "2hx",
                "Name": "ООО Криптэкс",
                "IsActive": true,
                "Features": [
                    {
                        "Name": "EnableRevocationV2",
                        "Description": "Аннулирование 1.02"
                    },
                    {
                        "Name": "SupportsAutoInvitation",
                        "Description": "Автоматическая обработка приглашений"
                    }
                ]
            }
        ]
    }