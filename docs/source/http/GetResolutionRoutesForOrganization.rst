GetResolutionRoutesForOrganization
==================================

Имя ресурса: **/GetResolutionRoutesForOrganization**

HTTP метод: **GET**

Параметры строки запроса:

-  *orgId*: идентификатор организации;

В запросе должен присутствовать HTTP-заголовок ``Authorization`` с необходимыми данными для :doc:`авторизации <../Authorization>`.

Метод возвращает список всех неудаленных маршрутов согласования для организации *orgId*.

В теле ответа содержится протобуфер :doc:`ResolutionRouteList <../proto/ResolutionRoute>`, который содержит в себе список протобуферов :doc:`ResolutionRoute <../proto/ResolutionRoute>`

.. code-block:: protobuf

    message ResolutionRouteList {
        repeated ResolutionRoute ResolutionRoutes = 1;
    }

    message ResolutionRoute {
        required string RouteId = 1;
        required string Name = 2;
    }

Возможные HTTP-коды возврата:

-  200 (OK) - операция успешно завершена;

-  400 (Bad Request) - данные в запросе имеют неверный формат или отсутствуют обязательные параметры;

-  401 (Unauthorized) - в запросе отсутствует HTTP-заголовок ``Authorization``, или в этом заголовке содержатся некорректные авторизационные данные;

-  403 (Forbidden) - доступ к ящику с предоставленным авторизационным токеном запрещен, либо у пользователя нет доступа к запрашиваемому документу;

-  404 (Not Found) - не найдена организация с идентификатором *orgId*;

-  405 (Method not allowed) - используется неподходящий HTTP-метод;

-  500 (Internal server error) - при обработке запроса возникла непредвиденная ошибка.
