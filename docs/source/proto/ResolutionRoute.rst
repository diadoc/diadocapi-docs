ResolutionRoute
===============

.. code-block:: protobuf

    message ResolutionRouteList {
        repeated ResolutionRoute ResolutionRoutes = 1;
    }

    message ResolutionRoute {
        required string RouteId = 1;
        required string Name = 2;
    }

Структура данных *ResolutionRoute* представляет один маршрут согласования в организации:

-  *RouteId* - уникальный идентификатор маршрута согласования

-  *Name* - имя маршрута согласования
