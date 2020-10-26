Подпись сертификатом без носителя
========================

Для подписания сертификатом без носителя нужно вызвать метод :doc:`http/DssSign`. В результате его выполнения вы получите идентификатор операции, а на телефон пользователя придет запрос на подтверждение. Затем надо периодически вызывать метод  :doc:`http/DssSignResult`, дождаться окончания операции и получить файлы подписи или статус о неуспешном завершении операции.

Пример с использованием C# SDK
------------------------------

.. code-block:: csharp

    var nameOnShelf1 = api.UploadFileToShelf(authToken, Encoding.UTF8.GetBytes("test 1"));
    var nameOnShelf2 = api.UploadFileToShelf(authToken, Encoding.UTF8.GetBytes("test 2"));

    var request = new DssSignRequest
    {
        Files = {
            new DssSignFile { FileName = "file1.txt", Content = new Content_v3 { NameOnShelf = "__userId__/" + nameOnShelf1 } },
            new DssSignFile { FileName = "file2.txt", Content = new Content_v3 { NameOnShelf = "__userId__/" + nameOnShelf2 } }
        }
    };

    var operation = api.DssSign(authToken, boxId, request, dssCertificateThumbprint);
    var stopwatch = Stopwatch.StartNew();
    while (true)
    {
        var result = api.DssSignResult(authToken, boxId, operation.TaskId);
        switch (result.OperationStatus)
        {
            case DssOperationStatus.Completed:
                Assert.That(result.FileSigningResults.Count, Is.EqualTo(2));
                return;
            case DssOperationStatus.InProgress:
                if (stopwatch.Elapsed > TimeSpan.FromMinutes(5)) throw new TimeoutException();
                Thread.Sleep(TimeSpan.FromSeconds(15));
                continue;
            default:
                throw new InvalidOperationException(string.Format("Signing has failed: {0}", result.OperationStatus);
        }
    }

HTTP-интерфейс
--------------

.. toctree::
   :name: toc3
   :maxdepth: 1
   :titlesonly:

   http/DssSign
   http/DssSignResult

Структуры данных
----------------

.. toctree::
   :name: toc4
   :maxdepth: 1
   :titlesonly:

   proto/AsyncMethodResult
   proto/DssSignRequest
   proto/DssSignResult

- :ref:`DssFileSigningResult <dss-file-signing-result>`
- :ref:`DssFileSigningStatus <dss-file-signing-status>`
- :ref:`DssOperationStatus <dss-operation-status>`
- :ref:`DssSignFile <dss-sign-file>`
