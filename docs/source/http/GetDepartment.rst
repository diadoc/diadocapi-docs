GetDepartment
=============

Имя ресурса: **/GetDepartment**

HTTP метод: **GET**

Параметры строки запроса:

-  *orgId*: идентификатор организации.

- *departmentId*: идентификатор подразделения организации.

-  *outputFormat*: формат вывода данных, может отсутствовать. Возможные значения: xml, protobuf (по-умолчанию - protobuf).

В запросе должен присутствовать HTTP-заголовок ``Authorization`` с необходимыми данными для :doc:`авторизации <../Authorization>`.

В теле ответа содержатся справочные данные для подразделения, сериализованные в запрошенном формате:

-  если в строке запроса не было параметра outputFormat, либо его значение было равно protobuf, данные возвращаются сериализованными в протобуфер :doc:`../proto/Department`;

-  если значение параметра outputFormat в строке запроса было равно xml, данные возвращаются в формате xml, как в следующем примере:

   ::

       <Department id="departmentId" parent-id="parentDepartmentId" name="Название" abbreviation="Н" kpp="123456789">
         <Address>
           <RussianAddress
             zip-code="620000"
             region="Свердловская область"
             territory=""
             city="Екатеринбург"
             locality=""
             street=""
             building=""
             block=""
             apartment="" />
         </Address>
       </Department>
       <Department id="departmentId" parent-id="parentDepartmentId" name="Название" abbreviation="Н" kpp="123456789">
         <Address>
           <ForeignAddress
             country="USA"
             address="Washington DC" />
         </Address>
       </Department>

Возможные HTTP-коды возврата:

-  200 (OK) - операция успешно завершена;

-  400 (Bad Request) - если не заданы или имеют неверный формат параметры orgId и departmentId;

-  401 (Unauthorized) - в запросе отсутствует HTTP-заголовок ``Authorization``, или в этом заголовке содержатся некорректные авторизационные данные;

-  404 (Not Found):

    - организация с указанным идентификатором не найдена в справочнике,

    - подразделение с указанным идентификатором не найдено в организации;

-  405 (Method not allowed) - используется неподходящий HTTP-метод;

-  500 (Internal server error) - при обработке запроса возникла непредвиденная ошибка.
