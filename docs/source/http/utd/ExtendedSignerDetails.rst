ExtendedSignerDetails
=====================

Набор полей для счетов-фактур/актов/торгов был значительно меньше, чем в УПД/УКД, и все данные подписанта можно было достать из сертификата и данных его организации. Это автоматическое заполнение данных подписанта происходило при заполнении *BoxId* и *Certificate/CertificateThumbprint*:

В теле запроса должно содержаться отправляемое сообщение, сериализованное в протобуфер :doc:`../../proto/utd/ExtendedSignerDetailsToPost`.

В теле ответа содержится отправленное сообщение, сериализованное в протобуфер :doc:`../../proto/utd/ExtendedSigner`.

.. http:post:: /ExtendedSignerDetails

   :query boxId: идентификатор ящика, для которого нужно заполнить данные о подписанте
   :query thumbprint: отпечаток сертификата, для которого нужно заполнить дополнтиельные данные о подписанте
   :query buyer: флаг, указывающий, что указанные данные должны использоваться при формировании титула покупателя
   :query forCorrection: флаг, указывающий, что указанные данные должны использоваться при формировании корректировки

   :reqheader Authorization: в запросе должен присутствовать HTTP-заголовок ``Authorization`` с необходимыми данными для :doc:`авторизации <../../Authorization>`
   :reqheader Content-Type: test
   :statuscode 200: операция успешно завершена
   :statuscode 400: данные в запросе имеют неверный формат или отсутствуют обязательные параметры
   :statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization``, или в этом заголовке содержатся некорректные авторизационные данные
   :statuscode 403: доступ к ящику с предоставленным авторизационным токеном запрещен
   :statuscode 405: используется неподходящий HTTP-метод
   :statuscode 500: при обработке запроса возникла непредвиденная ошибка

**Пример запроса**:

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
