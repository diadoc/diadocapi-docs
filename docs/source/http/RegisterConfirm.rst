RegisterConfirm
===============

.. http:post:: /RegisterConfirm

    :reqheader Authorization: необходимые данные для :doc:`авторизации <../Authorization>`

    :statuscode 200: операция успешно завершена
    :statuscode 400: данные в запросе имеют неверный формат, отсутствуют обязательные параметры или предоставлен невалидный контент подписи
    :statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization``, или в этом заголовке содержатся некорректные авторизационные данные
    :statuscode 405: используется неподходящий HTTP-метод
    :statuscode 409: текущее состояние регистрации не требует подтверждения
    :statuscode 500: при обработке запроса возникла непредвиденная ошибка

**Тело запроса:** :doc:`../proto/RegistrationConfirmRequest`

Позволяет подтвердить владение закрытым ключом сертификата для регистрации в организацию методом :doc:`Register`.

Примеры использования
---------------------

Примеры запросов
^^^^^^^^^^^^^^^^

С телом сертификата
~~~~~~~~~~~~~~~~~~~

.. sourcecode:: http

    POST /RegisterConfirm HTTP/1.1
    Host: diadoc-api.kontur.ru
    Authorization: DiadocAuth ddauth_api_client_id=key, ddauth_token=token
    Content-Type: application/json; charset=utf-8

    {
        "CertificateContent": "<certificateBytesBase64>",
        "DataToSign": "<dataToSignBytesBase64>",
        "Signature": "<signatureBytesBase64>"
    }

С отпечатком сертификата
~~~~~~~~~~~~~~~~~~~~~~~~

.. sourcecode:: http

    POST /RegisterConfirm HTTP/1.1
    Host: diadoc-api.kontur.ru
    Authorization: DiadocAuth ddauth_api_client_id=key, ddauth_token=token
    Content-Type: application/json; charset=utf-8

    {
        "Thumbprint": "B0E10292B0024E7197A76B741CE0D271FEAD7E10",
        "DataToSign": "<dataToSignBytesBase64>",
        "Signature": "<signatureBytesBase64>"
    }

Пример с использованием C# SDK
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: csharp

    var request = new RegistrationRequest
    {
        Thumbprint = certificate.Sha1Thumbprint
    };

    var response = api.Register(token, request);
        
    if (response.RegistrationStatus == RegistrationStatus.CertificateOwnershipProofIsRequired)
    {
        api.RegisterConfirm(
            token,
            new RegistrationConfirmRequest
            {
                Thumbprint = certificate.Sha1Thumbprint,
                DataToSign = response.DataToSign,
                Signature = Sign(response.DataToSign, certificate)
            });
            
         response = api.Register(token, request);
    }
    
    if (response.RegistrationStatus == RegistrationStatus.RegistrationIsInProcess)
    {
        Thread.Sleep(TimeSpan.FromSeconds(5));
        response = api.Register(token, request);
    }
    
    Console.WriteLine(string.Format("BoxId: {0}, Status: {1}", response.BoxId, response.RegistrationStatus);
