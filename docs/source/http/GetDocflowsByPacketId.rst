GetDocflowsByPacketId
======================

Метод ``GetDocflowsByPacketId`` возвращает список документов, находящихся в пакете.

.. http:post:: /V2/GetDocflowsByPacketId

	:queryparam boxId: идентификатор ящика организации.

	:requestheader Authorization: данные, необходимые для :doc:`авторизации <../Authorization>`.
	
	:request Body: Тело запроса должно содержать структуру :doc:`../proto/GetDocflowsByPacketIdRequest`.
	
	:statuscode 200: операция успешно завершена.
	:statuscode 400: данные в запросе имеют неверный формат или отсутствуют обязательные параметры.
	:statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization`` или в этом заголовке содержатся некорректные авторизационные данные.
	:statuscode 402: у организации с указанным идентификатором ``boxId`` закончилась подписка на API.
	:statuscode 403: доступ к ящику с предоставленным авторизационным токеном запрещен.
	:statuscode 405: используется неподходящий HTTP-метод.
	:statuscode 500: при обработке запроса возникла непредвиденная ошибка.

Метод возвращает список документов, представленный структурой :doc:`../proto/GetDocflowsByPacketIdResponse`.  В списке возвращаются только те документы, к которым у пользователя есть доступ.

Список документов в ответе может содержать не более 100 элементов. Если документов больше, их можно получить постранично. Для получения очередной страницы передайте в поле запроса :doc:`GetDocflowsByPacketIdRequest.AfterIndexKey <../proto/GetDocflowsByPacketIdRequest>` индекс последнего документа предыдущей страницы.

При вызове метода можно указать максимальное количество элементов на странице в поле :doc:`GetDocflowsByPacketIdRequest.Count <../proto/GetDocflowsByPacketIdRequest>`, но оно не должно превышать 100 элементов.

Метод не гарантирует, что все страницы, кроме последней, будут содержать одинаковое максимальное количество документов. При разработке интеграционного решения учитывайте, что в очередной странице может не быть ни одного документа.

SDK
"""

.. code-block:: csharp

    GetDocflowsByPacketIdResponse GetDocflowsByPacketId(string authToken, string boxId, GetDocflowsByPacketIdRequest request);

Пример использования (C#)
^^^^^^^^^^^^^^^^^^^^^^^^^

Постраничное получение документов из пакета.

.. code-block:: csharp

    byte[] pageKey = null;
    while (true)
    {
        var request = new GetDocflowsByPacketIdRequest
        {
            PacketId = packetId,
            AfterIndexKey = pageKey
        };
        var response = api.GetDocflowsByPacketId(token, boxId, request);
        pageKey = response.NextPageIndexKey;
        Console.Out.WriteLine("Fetched {0} documents", response.Documents.Count);
        if (response.NextPageIndexKey == null)
            break;
    }