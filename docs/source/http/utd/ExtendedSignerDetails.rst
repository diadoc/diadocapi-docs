ExtendedSignerDetails
=====================

.. warning::
   Этот метод устарел. Используйте метод :doc:`ExtendedSignerDetailsV2`.

Набор необходимых полей для подписания счетов-фактур, актов и накладных был значительно меньше, чем для подписания УПД и УКД.

Все данные подписанта можно было достать из сертификата и данных его организации - автоматическое заполнение данных подписанта происходило при заполнении *BoxId* и *Certificate/CertificateThumbprint*.

Данная логика сохранилась и при подписании УПД и УКД. Автоматическое заполнение происходит, если в Диадоке есть дополнительные данные, необходимые для подписания. Если дополнительных данных, необходимых для подписания в Диадоке нет, то будет возникать ошибка.

Заполнение данных
-----------------

Расширенные данные можно заполнить методом *ExtendedSignerDetails*.

В теле запроса должно содержаться отправляемое сообщение, сериализованное в протобуфер :doc:`../../proto/utd/ExtendedSignerDetailsToPost`.

В теле ответа содержится отправленное сообщение, сериализованное в протобуфер :doc:`../../proto/utd/ExtendedSigner`.

.. http:post:: /ExtendedSignerDetails

	:queryparam boxId: идентификатор ящика, для которого нужно заполнить данные о подписанте.
	:queryparam thumbprint: отпечаток сертификата, для которого нужно заполнить дополнительные данные о подписанте.
	:queryparam buyer: флаг, указывающий, что указанные данные должны использоваться при формировании титула покупателя.
	:queryparam correction: флаг, указывающий, что указанные данные должны использоваться при формировании корректировки.

	:requestheader Authorization: данные, необходимые для :doc:`авторизации <../../Authorization>`.

	:statuscode 200: операция успешно завершена.
	:statuscode 400: данные в запросе имеют неверный формат или отсутствуют обязательные параметры.
	:statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization`` или в этом заголовке содержатся некорректные авторизационные данные.
	:statuscode 403: доступ к ящику с предоставленным авторизационным токеном запрещен.
	:statuscode 405: используется неподходящий HTTP-метод.
	:statuscode 500: при обработке запроса возникла непредвиденная ошибка.

Проверка данных
---------------

Проверить, какие дополнительные данные указаны для конкретного подписанта можно этим же методом.

В теле ответа содержится отправленное сообщение, сериализованное в протобуфер :doc:`../../proto/utd/ExtendedSigner`.

.. http:get:: /ExtendedSignerDetails

   :queryparam boxId: идентификатор ящика, для которого нужно заполнить данные о подписанте.
   :queryparam thumbprint: отпечаток сертификата, для которого нужно заполнить дополнтиельные данные о подписанте.
   :queryparam buyer: флаг, указывающий, что указанные данные должны использоваться при формировании титула покупателя.
   :queryparam correction: флаг, указывающий, что указанные данные должны использоваться при формировании корректировки.

   :requestheader Authorization: данные, необходимые для :doc:`авторизации <../../Authorization>`.
   
   :statuscode 200: операция успешно завершена.
   :statuscode 400: данные в запросе имеют неверный формат или отсутствуют обязательные параметры.
   :statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization`` или в этом заголовке содержатся некорректные авторизационные данные.
   :statuscode 403: доступ к ящику с предоставленным авторизационным токеном запрещен.
   :statuscode 405: используется неподходящий HTTP-метод.
   :statuscode 500: при обработке запроса возникла непредвиденная ошибка.


Примеры
-------

**Пример POST запроса**:

   .. sourcecode:: http

      POST /ExtendedSignerDetails?boxId=48ad04b4-af63-4a72-901c-f19b698c31cc&thumbprint=B8C080A89A5F643A&buyer=true HTTP/1.1
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
