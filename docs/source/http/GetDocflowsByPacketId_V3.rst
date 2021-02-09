GetDocflowsByPacketId (версия 3)
================================

Метод возвращает список документов, находящихся в указанном пакете.

Если документов достаточно много, их выгрузку можно осуществлять постранично. Для получения очередной страницы в метод передается специальный ключ, указывающий на начало этой страницы. Максимальный размер страницы можно указать при запросе, однако это число не должно превышать 100 (значение по умолчанию). Метод не гарантирует, что все страницы, кроме последней, будут содержать одинаковое максимальное количество документов. Интеграционное решение должно быть рассчитано на то, что в рамках очередной страницы не будет выгружено ни одного документа.

В выдачу метода попадают только те документы, к которым у текущего пользователя есть доступ.

HTTP
~~~~

.. http:post:: /V3/GetDocflowsByPacketId

    :query boxId: идентификатор ящика

    :reqheader Authorization: необходимые данными для :doc:`авторизации <../Authorization>`

    :statuscode 200: операция успешно завершена
    :statuscode 400: данные в запросе имеют неверный формат или отсутствуют обязательные параметры
    :statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization``, или в этом заголовке содержатся некорректные авторизационные данные
    :statuscode 403: доступ к ящику с предоставленным авторизационным токеном запрещен
    :statuscode 405: используется неподходящий HTTP-метод
    :statuscode 500: при обработке запроса возникла непредвиденная ошибка

**Тело запроса:** протобуфер :doc:`../proto/GetDocflowsByPacketIdRequest`.

**Тело ответа:** протобуфер :doc:`../proto/GetDocflowsByPacketIdResponseV3`.

SDK
~~~

.. code-block:: csharp

    GetDocflowsByPacketIdResponseV3 GetDocflowsByPacketId(string authToken, string boxId, GetDocflowsByPacketIdRequest request);

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
        var response = api.Docflow.GetDocflowsByPacketId(token, boxId, request);
        pageKey = response.NextPageIndexKey;
        Console.Out.WriteLine("Fetched {0} documents", response.Documents.Count);
        if (response.NextPageIndexKey == null)
            break;
    }
