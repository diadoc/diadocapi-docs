ExtendedSignerDetails
=====================

Набор необходимых полей для подписания счетов-фактур, актов и накладных был значительно меньше, чем для подписания УПД и УКД.

Все данные подписанта можно было достать из сертификата и данных его организации - автоматическое заполнение данных подписанта происходило при заполнении *BoxId* и *Certificate/CertificateThumbprint*.

Данная логика сохранилась и при подписании УПД/УКД и актов/накладных в форматах 551/552. Автоматическое заполнение происходит, если в Диадоке есть дополнительные данные, необходимые для подписания. Если дополнительных данных, необходимых для подписания в Диадоке нет, то будет возникать ошибка.

Расширенные данные можно заполнить методом *ExtendedSignerDetails*.

Заполнение данных
-----------------

Во второй версии метода *ExtendedSignerDetails* параметры *buyer* и *correction* заменены на один параметр целочисленного типа *documentTitleType*. Возможные значения параметра представлены ниже:

::

    DocumentTitleType {
        UtdSeller = 0;            // Данные для титула продавца УПД
        UtdBuyer = 1;             // Данные для титула покупателя УПД
        UcdSeller = 2;            // Данные для титула продавца УКД
        UcdBuyer = 3;             // Данные для титула покупателя УКД
        TovTorg551Seller = 4;     // Данные для титула продавца 551
        TovTorg551Buyer = 5;      // Данные для титула покупателя 551
        AccCert552Seller = 6;     // Данные для титула исполнителя 552
        AccCert552Buyer = 7;      // Данные для титула заказчика 552
        Utd820Buyer = 8;          // Данные для титула покупателя УПД формата приказа 820
        Torg2Buyer = 9;           // Данные для титула покупателя Торг-2
        Torg2AdditionalInfo = 10; // Данные для титула продавца Торг-2
        Ucd736Buyer = 11;         // Данные для титула покупателя УКД формата приказа 736
    }


В теле запроса должно содержаться отправляемое сообщение, сериализованное в протобуфер :doc:`../../proto/utd/ExtendedSignerDetailsToPost`.

В теле ответа содержится отправленное сообщение, сериализованное в протобуфер :doc:`../../proto/utd/ExtendedSigner`.

.. http:post:: /V2/ExtendedSignerDetails

   :query string boxId: идентификатор ящика, для которого нужно заполнить данные о подписанте
   :query string thumbprint: отпечаток сертификата, для которого нужно заполнить дополнительные данные о подписанте
   :query int documentTitleType: тип титула, для которого нужно заполнить дополнительные данные о подписанте

   :reqheader Authorization: в запросе должен присутствовать HTTP-заголовок ``Authorization`` с необходимыми данными для :doc:`авторизации <../../Authorization>`
   :reqheader Content-Type: test
   :statuscode 200: операция успешно завершена
   :statuscode 400: данные в запросе имеют неверный формат или отсутствуют обязательные параметры
   :statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization``, или в этом заголовке содержатся некорректные авторизационные данные
   :statuscode 403: доступ к ящику с предоставленным авторизационным токеном запрещен
   :statuscode 405: используется неподходящий HTTP-метод
   :statuscode 500: при обработке запроса возникла непредвиденная ошибка


Проверка данных
---------------

Проверить, какие дополнительные данные указаны для конкретного подписанта можно этим же методом.

В теле ответа содержится отправленное сообщение, сериализованное в протобуфер :doc:`../../proto/utd/ExtendedSigner`.

.. http:get:: /V2/ExtendedSignerDetails

   :query string boxId: идентификатор ящика, для которого нужно заполнить данные о подписанте
   :query string thumbprint: отпечаток сертификата, для которого нужно заполнить дополнтиельные данные о подписанте
   :query int documentTitleType: тип титула, для которого нужно заполнить дополнительные данные о подписанте

   :reqheader Authorization: в запросе должен присутствовать HTTP-заголовок ``Authorization`` с необходимыми данными для :doc:`авторизации <../../Authorization>`
   :reqheader Content-Type: test
   :statuscode 200: операция успешно завершена
   :statuscode 400: данные в запросе имеют неверный формат или отсутствуют обязательные параметры
   :statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization``, или в этом заголовке содержатся некорректные авторизационные данные
   :statuscode 403: доступ к ящику с предоставленным авторизационным токеном запрещен
   :statuscode 405: используется неподходящий HTTP-метод
   :statuscode 500: при обработке запроса возникла непредвиденная ошибка

Примеры
-------

**Пример POST запроса**:

   .. sourcecode:: http

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
