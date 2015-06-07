GetDocflowsByPacketId
======================

Метод возвращает список документов, находящихся в указанном пакете.

Если документов достаточно много, их выгрузку можно осуществлять постранично. Для получения очередной страницы в метод передается специальный ключ, указывающий на начало этой страницы. Максимальный размер страницы можно указать при запросе, однако это число не должно превышать 100 (значение по умолчанию). Метод не гарантирует, что все страницы, кроме последней, будут содержать одинаковое максимальное количество документов. Интеграционное решение должно быть рассчитано на то, что в рамках очередной страницы не будет выгружено ни одного документа.

В выдачу метода попадают только те документы, к которым у текущего пользователя есть доступ.

HTTP
~~~~

**POST /V2/GetDocflowsByPacketId**

**Параметры запроса:**

-  *boxId* - идентификатор ящика

**Тело запроса:** протобуфер :doc:`../proto/GetDocflowsByPacketIdRequest`.

**Тело ответа:** протобуфер :doc:`../proto/GetDocflowsByPacketIdResponse`.

**Возможные HTTP-коды возврата:**

-  *200 (OK)* - операция успешно завершена.
-  *400 (Bad Request)* - данные в запросе имеют неверный формат или отсутствуют обязательные параметры.
-  *401 (Unauthorized)* - в запросе отсутствует HTTP-заголовок ``Authorization``, или в этом заголовке содержатся некорректные авторизационные данные.
-  *403 (Forbidden)* - доступ к ящику с предоставленным авторизационным токеном запрещен.
-  *405 (Method not allowed)* - используется неподходящий HTTP-метод.
-  *500 (Internal server error)* - при обработке запроса возникла непредвиденная ошибка.

SDK
~~~

.. code-block:: csharp

    GetDocflowsByPacketIdResponse GetDocflowsByPacketId(string authToken, string boxId, GetDocflowsByPacketIdRequest request);

Пример использования (C#)
^^^^^^^^^^^^^^^^^^^^^^^^^

Постраничная выгрузка документов из пакета:

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
