Работа с организациями
======================

Для упрощения работы с API существует SDK (C#/C++/Java/COM), скрывающий детали взаимодействия по HTTP и позволяющий работать с API через набор функций.

HTTP-интерфейс
--------------

.. toctree::
   :name: toc3
   :maxdepth: 2
   :titlesonly:

   http/GetBox
   http/GetDepartment
   http/GetMyOrganizations
   http/GetMyPermissions
   http/GetMyUser
   http/GetOrganization
   http/GetOrganizationsByInnKpp
   http/GetOrganizationsByInnList
   http/GetOrganizationUsers
   http/ParseRussianAddress
   

Структуры данных
----------------

.. toctree::
   :name: toc4
   :maxdepth: 2
   :titlesonly:

   proto/Address
   proto/Department
   proto/GetOrganizationsByInnListRequest
   GetOrganizationsByInnListResponse <proto/GetOrganizationsByInnListRequest>
   proto/Organization
   proto/OrganizationInfo
   proto/OrganizationUser
   proto/OrganizationUserPermissions
   proto/User