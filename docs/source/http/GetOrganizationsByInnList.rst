GetOrganizationsByInnList
=========================

Метод позволяет для организации по списку ИНН получить статус контрагентов в Диадоке.

Имя ресурса: **/GetOrganizationsByInnList**

HTTP метод: **POST**

Параметры строки запроса:

-  *myOrgId*: идентификатор организации, для которой нужно получить статус ее контрагентов;

В запросе должен присутствовать HTTP-заголовок ``Authorization`` с необходимыми данными для :doc:`авторизации <../Authorization>`.

В теле запроса должна содержатся структура :doc:`../proto/GetOrganizationsByInnListRequest`

В теле ответа содержится структура :doc:`GetOrganizationsByInnListResponse <../proto/GetOrganizationsByInnListRequest>`

Если при вызове метода не передан параметр строки запроса *myOrgId*, то в теле ответа возравщается структура :doc:`GetOrganizationsByInnListResponse <../proto/GetOrganizationsByInnListRequest>`, где для вложенной структуры  :doc:`OrganizationWithCounteragentStatus <../proto/GetOrganizationsByInnListRequest>` значения поля *CounteragentStatus* всегда будет равно значению по умолчанию - *UnknownCounteragentStatus*.

Возможные HTTP-коды возврата:

-  *200 (OK)* - операция успешно завершена;

-  *400 (Bad Request)* - данные в запросе имеют неверный формат или отсутствуют обязательные параметры;

-  *401 (Unauthorized)* - в запросе отсутствует HTTP-заголовок ``Authorization``, или в этом заголовке содержатся некорректные авторизационные данные;

-  *405 (Method not allowed)* - используется неподходящий HTTP-метод;

-  *500 (Internal server error)* - при обработке запроса возникла непредвиденная ошибка.