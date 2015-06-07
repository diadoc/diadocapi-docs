GetMyOrganizations
==================

Имя ресурса: **/GetMyOrganizations**

HTTP метод: **GET**

Параметры строки запроса:

-  *outputFormat*: формат вывода данных, может отсутствовать. Возможные значения: xml, protobuf (по-умолчанию - protobuf).

В запросе должен присутствовать HTTP-заголовок ``Authorization`` с необходимыми данными для :doc:`авторизации <../Authorization>`.

В теле ответа содержится список всех ящиков, к которым имеет доступ пользователь-владелец авторизационного токена, сериализованный в заданном формате:

-  если в строке запроса не было параметра outputFormat, либо его значение было равно protobuf, то данные возвращаются сериализованными в протобуфер :doc:`OrganizationList <../proto/Organization>`;

-  если значение параметра outputFormat в строке запроса было равно xml, то данные возвращаются в формате xml, как в следующем примере:

   ::

       <Organizations>
         <Organization id="orgId1" inn="1234567890" kpp="123456789" fullName="ООО Яблоко" shortName="ООО Яблоко" joinedDiadocTreaty="true">
           <Boxes>
             <Box id="boxId1" title="Ящик для счетов фактур" />
             <Box id="boxId2" title="Тестовый ящик" />
           </Boxes>
         </Organization>
         <Organization id="orgId2" inn="123456789012" kpp="" fullName="ИП Сидоров Иван Петрович" shortName="" joinedDiadocTreaty="false">
           <Boxes>
             <Box id="boxId3" title="Основной ящик" />
           </Boxes>
         </Organization>
       </Organizations>

Возможные HTTP-коды возврата:

-  200 (OK) - операция успешно завершена;

-  401 (Unauthorized) - в запросе отсутствует HTTP-заголовок ``Authorization``, или в этом заголовке содержатся некорректные авторизационные данные;

-  405 (Method not allowed) - используется неподходящий HTTP-метод;

-  500 (Internal server error) - при обработке запроса возникла непредвиденная ошибка.