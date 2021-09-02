Документация API
================

|image0|_

Диадок – юридически значимый онлайн-документооборот между организациями.

Интеграция с помощью API Диадока подойдет любым нестандартным учетным системам, для которых нет типового решения или оно не устраивает организацию. В результате интеграции в учетной системе появится та функциональность Диадока, которая нужна организации.

Возможности API Диадока
=======================

- Создание документов в xml-формате, утвержденном ФНС
- Отправка и получение документов из своей информационной системы
- Автоматическое подписание документов КЭП
- Актуальные статусы документов онлайн
- Работа со списком контрагентов
- Согласование документов
- Выборка документов по заданным в поиске параметрам

.. toctree::
   :maxdepth: 2
   :hidden:
   :titlesonly:
   :caption: История изменений

   ReleaseNotes
   
.. toctree::
   :maxdepth: 2
   :hidden:
   :titlesonly:
   :caption: С чего начать
   
   howtostart/IntegrationOptions
   
.. toctree::
   :maxdepth: 2
   :hidden:
   :titlesonly:
   :caption: Общее описание возможностей

   Overview
   IntegrationOptions_obsolete
   DataModel
   ApiClientOperationPrinciple
   Counteragents
   MiscellaneousApiFeatures

.. toctree::
   :maxdepth: 2
   :hidden:
   :titlesonly:
   :caption: Документооборот

   docflows/AttachmentVersion
   http/GetDocumentTypes
   docflows/InvoiceDocflow
   docflows/Torg12Docflow
   docflows/AktDocflow
   docflows/UtdDocflow
   docflows/NonformalizedDocflow
   docflows/TemplateDocflow

.. toctree::
   :maxdepth: 2
   :hidden:
   :titlesonly:
   :caption: Примеры использования

   howto/marking_ttgis
   howto/utd820
   howto/example_authorization
   howto/example_send_invoice
   howto/example_receive_invoice
   howto/example_torg12
   howto/example_acceptance_certificate

.. toctree::
   :maxdepth: 2
   :hidden:
   :titlesonly:
   :caption: Техническая документация

   DataStructures
   Authorization
   API_Invoices
   API_UniversalTransferDocument
   API_Documents
   API_Messages
   API_Events
   API_Organizations
   API_Departments
   API_Employees
   API_Counteragents
   API_Templates
   API_Registration
   Docflow API
   CloudSignApi
   API_Dss

.. toctree::
   :maxdepth: 2
   :hidden:
   :titlesonly:
   :caption: Справочное руководство

   http_methods
   protos
   lists

.. |image0| image:: _static/diadoc-logo.png
.. _image0: https://www.diadoc.ru/
