SearchDocflows (версия 3)
=========================

Метод ``SearchDocflows`` производит поиск документа по строке запроса.

.. http:post:: /V3/SearchDocflows

	:queryparam boxId: идентификатор ящика организации.

	:requestheader Authorization: данные, необходимые для :doc:`авторизации <../Authorization>`.

	:request Body: Тело запроса должно содержать структуру :doc:`../proto/SearchDocflowsRequest`.

	:statuscode 200: операция успешно завершена.
	:statuscode 400: данные в запросе имеют неверный формат или отсутствуют обязательные параметры.
	:statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization`` или в этом заголовке содержатся некорректные авторизационные данные.
	:statuscode 402: у организации с указанным идентификатором ``boxId`` закончилась подписка на API.
	:statuscode 403: доступ к ящику с предоставленным авторизационным токеном запрещен.
	:statuscode 405: используется неподходящий HTTP-метод.
	:statuscode 500: при обработке запроса возникла непредвиденная ошибка.

	:response Body: Тело ответа содержит список документов, представленный структурой :doc:`../proto/SearchDocflowsResponseV3`.
	
В ответе вернутся только те документы, к которым у пользователя есть доступ.

Метод разбивает строку запроса :doc:`SearchDocflowsRequest.QueryString <../proto/SearchDocflowsRequest>` следующими способами:

- Метод разбивает строку на токены по пробелам и разделительным символам. В ответ метода попадают документы, у которых хотя бы один из полученных токенов содержится в номере, дате, имени файла или других данных. 
- Если строка запроса имеет вид «ключ: значение», то метод разбивает строку в соответствии с форматом YAML. В ответ метода попадут документы, которые содержат указанную пару «ключ-значение» среди пользовательских данных, привязанных к документу.

Список документов в ответе может содержать не более 100 элементов. Если документов больше, их можно получить постранично. Для получения очередной страницы передайте в поле запроса :doc:`SearchDocflowsRequest.FirstIndex <../proto/SearchDocflowsRequest>` индекс документа, с которого нужно начать выгрузку.

При вызове метода можно указать максимальное количество элементов на странице в поле :doc:`SearchDocflowsRequest.Count <../proto/SearchDocflowsRequest>`, но оно не должно превышать 100 элементов.

Метод не гарантирует, что все страницы, кроме последней, будут содержать одинаковое максимальное количество документов. При разработке интеграционного решения учитывайте, что в очередной странице может не быть ни одного документа.

SDK
"""

.. code-block:: csharp

    SearchDocflowsResponseV3 SearchDocflows(string authToken, string boxId, SearchDocflowsRequest request);

Пример использования (C#)
^^^^^^^^^^^^^^^^^^^^^^^^^

Постраничное получение документов, содержащих строку «Пример».

.. code-block:: csharp

    var request = new SearchDocflowsRequest { QueryString = "Пример" };
    while (true)
    {
        var response = api.Docflow.SearchDocflows(token, boxId, request);
        Console.Out.WriteLine("Fetched {0} documents", response.Documents.Count);
        if (!response.HaveMoreDocuments)
            break;
        request.FirstIndex += response.Documents.Count;
    }