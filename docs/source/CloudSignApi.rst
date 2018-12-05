Подпись Контур.Сертификатом
===========================

Подписание Контур.Сертификатом ЭП осуществляется в два этапа.

Во-первых, надо вызвать метод :doc:`http/CloudSign` и дождаться  его успешного завершения периодически вызывая метод :doc:`http/CloudSignResult`.

В результате успешного завершения этого этапа, вы получите token (идентификатор операции с Контур.Сертификатом ЭП), а на телефон пользователя будет отправлено SMS-сообщение с кодом подтверждения операции.

Во-вторых, надо вызывать метод :doc:`http/CloudSignConfirm` и передать в него полученный token и SMS-код. Затем, вызывая метод :doc:`http/CloudSignConfirmResult`, дождаться окончания операции и получить, либо подписи, либо код ошибки.

Ниже приведен пример кода на C#

.. code-block:: csharp

    //Загружаем данные на полку
    var nameOnShelf1 = api.UploadFileToShelf(authToken, Encoding.UTF8.GetBytes("TEST document 1"));
    var nameOnShelf2 = api.UploadFileToShelf(authToken, Encoding.UTF8.GetBytes("TEST document 2"));

    //Подписание
    var request = new CloudSignRequest {
        Files = {
            new CloudSignFile{ FileName = "File 1.txt", Content = new Content_v2{ NameOnShelf = nameOnShelf1 } },
            new CloudSignFile{ FileName = "File 2.txt", Content = new Content_v2{ NameOnShelf = nameOnShelf2 } },
        }
    };
    var aResult = api.CloudSign(authToken, request, cloudCertificateThumbprint);
    var cloudSignResult = api.WaitCloudSignResult(authToken, aResult.TaskId);

    //Запрашиваем у пользователя SMS-код подтверждения confirmationCode
    //Подтверждаем операцию подписи
    aResult = api.CloudSignConfirm(authToken, cloudSignResult.Token, confirmationCode);
    var cloudSignConfirmResult = api.WaitCloudSignConfirmResult(authToken, aResult.TaskId);

    //Получаем подписи
    Assert.AreEqual(2, cloudSignConfirmResult.Signatures.Count);
	
HTTP-интерфейс
--------------

.. toctree::
   :name: toc3
   :maxdepth: 1
   :titlesonly:

   http/CloudSign
   http/CloudSignConfirm
   http/CloudSignConfirmResult
   http/CloudSignResult
   http/AutoSignReceipts
   http/AutoSignReceiptsResult

Структуры данных
----------------

.. toctree::
   :name: toc4
   :maxdepth: 1
   :titlesonly:

   proto/AsyncMethodResult
   proto/CloudSignRequest
   proto/CloudSignConfirmResultDTO
   proto/CloudSignResultDTO
   proto/AutosignReceiptsResult
