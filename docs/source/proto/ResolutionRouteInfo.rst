ResolutionRouteInfo
=====================

.. code-block:: protobuf

    message ResolutionRouteAssignmentInfo {
        required string RouteId = 1;
	required string Author = 2;
    }

    message ResolutionRouteRemovalInfo {
        required string RouteId = 1;
	required string Author = 2;
    }
        

Структура данных *ResolutionRouteAssignmentInfo* содержит информацию о запуске документа по маршруту согласования:

-  *RouteId* - идентификатор маршрута согласования, по которому был запущен документ.

-  *Author* - ФИО сотрудника, запустившего документ по маршруту согласования.

Структура данных *ResolutionRouteRemovalInfo* содержит информацию о снятии документа с маршрута согласования:

-  *RouteId* - идентификатор маршрута согласования, с которого был снят документ.

-  *Author* - ФИО сотрудника, который снял документ с маршрута.
