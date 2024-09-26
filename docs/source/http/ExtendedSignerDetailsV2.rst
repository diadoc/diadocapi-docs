ExtendedSignerDetails
=====================

Набор необходимых полей для подписания счетов-фактур, актов и накладных был значительно меньше, чем для подписания УПД и УКД.

Все данные подписанта можно было достать из сертификата и данных его организации - автоматическое заполнение данных подписанта происходило при заполнении *BoxId* и *Certificate/CertificateThumbprint*.

Данная логика сохранилась и при подписании УПД/УКД и актов/накладных в форматах 551/552. Автоматическое заполнение происходит, если в Диадоке есть дополнительные данные, необходимые для подписания. Если дополнительных данных, необходимых для подписания в Диадоке нет, то будет возникать ошибка.

Расширенные данные можно заполнить методом *ExtendedSignerDetails*.

Заполнение данных
-----------------

Во второй версии метода *ExtendedSignerDetails* параметры *buyer* и *correction* заменены на один параметр целочисленного типа :doc:`../proto/DocumentTitleType``.

.. http:post:: /V2/ExtendedSignerDetails

   :queryparam string boxId: идентификатор :doc:`ящика <../../entities/box>` организации, для которого нужно заполнить данные о подписанте.
   :queryparam string thumbprint: отпечаток сертификата, для которого нужно заполнить дополнительные данные о подписанте.
   :queryparam int documentTitleType: тип титула, для которого нужно заполнить дополнительные данные о подписанте.

   :requestheader Authorization: данные, необходимые для :doc:`авторизации <../../Authorization>`.
   
   :request Body: Тело запроса должно содержать отправляемое сообщение, сериализованное в протобуфер :doc:`../../proto/ExtendedSignerDetailsToPost`.
   
   :statuscode 200: операция успешно завершена.
   :statuscode 400: данные в запросе имеют неверный формат или отсутствуют обязательные параметры.
   :statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization`` или в этом заголовке содержатся некорректные авторизационные данные.
   :statuscode 402: у организации с указанным идентификатором ``boxId`` закончилась подписка на API.
   :statuscode 403: доступ к ящику с предоставленным авторизационным токеном запрещен.
   :statuscode 405: используется неподходящий HTTP-метод.
   :statuscode 500: при обработке запроса возникла непредвиденная ошибка.

   :response Body: Тело ответа содержит отправленное сообщение, сериализованное в протобуфер :doc:`../../proto/ExtendedSignerDetails`.

Проверка данных
---------------

Проверить, какие дополнительные данные указаны для конкретного подписанта можно этим же методом.

.. http:get:: /V2/ExtendedSignerDetails

	:queryparam string boxId: идентификатор :doc:`ящика <../../entities/box>` организации, для которого нужно заполнить данные о подписанте
	:queryparam string thumbprint: отпечаток сертификата, для которого нужно заполнить дополнтиельные данные о подписанте
	:queryparam int documentTitleType: тип титула, для которого нужно заполнить дополнительные данные о подписанте

	:requestheader Authorization: данные, необходимые для :doc:`авторизации <../../Authorization>`.

	:statuscode 200: операция успешно завершена.
	:statuscode 400: данные в запросе имеют неверный формат или отсутствуют обязательные параметры.
	:statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization`` или в этом заголовке содержатся некорректные авторизационные данные.
	:statuscode 403: доступ к ящику с предоставленным авторизационным токеном запрещен.
	:statuscode 405: используется неподходящий HTTP-метод.
	:statuscode 500: при обработке запроса возникла непредвиденная ошибка.

	:response Body: Тело ответа содержит отправленное сообщение, сериализованное в протобуфер :doc:`../../proto/ExtendedSigner`.
	
Примеры
-------

**Пример POST запроса**:

   .. code-block:: http

      POST /V2/ExtendedSignerDetails?boxId=48ad04b4-af63-4a72-901c-f19b698c31cc&thumbprint=B8C080A89A5F643A&documentTitleType=0 HTTP/1.1
      Host: diadoc-api.kontur.ru
      Authorization: DiadocAuth ddauth_api_client_id=key, ddauth_token=token
      Content-Type: application/json; charset=utf-8

      {
         "JobTitle": "сотрудник",
         "SignerType": "LegalEntity",
         "SignerInfo": "additional",
         "SignerPowers": "PersonMadeOperation",
         "SignerStatus": "SellerEmployee",
         "SignerPowersBase": "Должностные обязанности"
      }

   **Пример ответа**:

   .. code-block:: http

      HTTP/1.1 200 OK
      Content-Type: application/json; charset=utf-8

      {
         "Surname": "Иванов",
         "FirstName": "Иван",
         "Patronymic": "Иванович",
         "JobTitle": "сотрудник",
         "Inn": "101010101010",
         "SignerType": "IndividualEntity",
         "SignerOrganizationName": "ЗАО \"ПФ \"СКБ Контур\"",
         "SignerInfo": "additional",
         "SignerPowers": "PersonMadeOperation",
         "SignerStatus": "SellerEmployee",
         "SignerPowersBase": "Должностные обязанности"
      }


----

.. rubric:: См. также

*Устаревшие версии метода:*
	- :doc:`obsolete/ExtendedSignerDetails`