Документация API
================

|image0|_

Диадок – это система обмена юридически-значимыми электронными документами между организациями.

Базовым уровнем интеграции с Диадоком является его **HTTP-API** интерфейс.

Для разработчиков, занимающихся интеграцией Диадока с различными программными продуктами, построенными на платформе 1С, доступен специальный внешний компонент.

.. toctree::
   :name: others
   :caption: История изменений
   :titlesonly:

   ReleaseNotes

.. toctree::
   :name: main
   :maxdepth: 1
   :caption: Общее описание возможностей

   Обзор возможностей API <Overview>
   Возможности для интеграции <IntegrationOptions>
   Модель данных <DataModel>
   Порядок работы с API <ApiClientOperationPrinciple>
   Управление списком активных контрагентов <Counteragents>
   Дополнительные функции API <MiscellaneousApiFeatures>

.. toctree::
   :name: docflow
   :maxdepth: 1
   :caption: Документооборот

   Форматы документов <docflows/AttachmentVersion>
   Типы документов <http/GetDocumentTypes>
   Документооборот счетов-фактур <docflows/InvoiceDocflow>
   Документооборот накладных <docflows/Torg12Docflow>
   Документооборот актов <docflows/AktDocflow>
   Документооборот УПД <docflows/UtdDocflow>
   Неформализованный документооборот <docflows/NonformalizedDocflow>
   Документооборот шаблонов <docflows/TemplateDocflow>

.. toctree::
   :name: examples
   :maxdepth: 1
   :caption: Примеры использования

   Как авторизоваться в системе <howto/example_authorization>
   Как отправить счет-фактуру <howto/example_send_invoice>
   Как получить счет-фактуру <howto/example_receive_invoice>
   Как отправить и получить товарную накладную ТОРГ-12 <howto/example_torg12>
   Как отправить и получить акт о выполнении работ/оказании услуг <howto/example_acceptance_certificate>

.. toctree::
   :name: work
   :maxdepth: 1
   :caption: Техническая документация

   Структуры данных <DataStructures>
   Авторизация <Authorization>
   Работа с СФ/ИСФ/КСФ <API_Invoices>
   Работа с УПД/УКД <API_UniversalTransferDocument>
   Работа с документами <API_Documents>
   Работа с сообщениями <API_Messages>
   Работа с событиями <API_Events>
   Работа с организациями <API_Organizations>
   Работа с подразделениями <API_Departments>
   Работа с сотрудниками <API_Employees>
   Работа с контрагентами <API_Counteragents>
   Работа с шаблонами <API_Templates>
   Регистрация организации и сотрудника по сертификату <API_Registration>
   Docflow API <Docflow API>
   Электронная подпись Контур.Сертификатом <CloudSignApi>

.. rubric:: Справочное руководство

-  :doc:`Справочник HTTP-интерфейсов <http_methods>`
-  :doc:`Справочник структур данных <protos>`
-  :doc:`Список HTTP-интерфейсов и структур данных <lists>`

..
  .. toctree::
     :name: tech
     :maxdepth: 1
     :caption: Справочное руководство

     http_methods
     protos
     lists

.. |image0| image:: _static/diadoc-logo.png
.. _image0: https://www.diadoc.ru/
