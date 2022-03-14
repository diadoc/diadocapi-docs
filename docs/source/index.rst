Документация API
================

.. |diadoc_logo| image:: _static/diadoc-logo.png
.. _diadoc_logo: https://www.diadoc.ru/
|diadoc_logo|_

Диадок — юридически значимый онлайн-документооборот между организациями.

API Диадока — универсальный инструмент для интеграции учетных систем с Диадоком. API позволяет организации разработать собственное решение и реализовать в нем необходимую функциональность.

На основе API построены некоторые :doc:`готовые решения <howtostart/IntegrationOptions>`, которые можно использовать при разработке клиентских приложений.

Возможности API Диадока
=======================

- Создание документов в xml-формате, утвержденном ФНС
- Отправка и получение документов из своей учетной системы
- Автоматическое подписание документов КЭП
- Согласование документов
- Актуальные статусы документов онлайн
- Выборка документов по заданным в поиске параметрам
- Работа со списком контрагентов


.. toctree::
	:maxdepth: 1
	:titlesonly:
	:caption: История изменений

	ReleaseNotes
   
.. toctree::
	:maxdepth: 1
	:titlesonly:
	:caption: С чего начать

	howtostart/IntegrationOptions
   
.. toctree::
	:maxdepth: 1
	:titlesonly:
	:caption: Общее описание возможностей

	Overview
	IntegrationOptions_obsolete
	DataModel
	ApiClientOperationPrinciple
	Counteragents
	MiscellaneousApiFeatures

.. toctree::
	:maxdepth: 1
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
	:maxdepth: 1
	:titlesonly:
	:caption: Примеры использования

	howto/powerofattorney
	howto/marking_ttgis
	howto/utd820
	howto/example_authorization
	howto/example_send_invoice
	howto/example_receive_invoice
	howto/example_torg12
	howto/example_acceptance_certificate

.. toctree::
	:maxdepth: 1
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
	:maxdepth: 1
	:titlesonly:
	:caption: Справочное руководство

	http_methods
	protos
	lists
