Документация API
================

.. |diadoc_logo| image:: _static/diadoc-logo.png
.. _diadoc_logo: https://www.diadoc.ru/
|diadoc_logo|_

Диадок — система обмена юридически-значимыми электронными документами между организациями.

`API Диадока <howtostart/IntegrationOptions.html#http-api>`__ — универсальный инструмент для интеграции учетных систем с Диадоком. API позволяет организации разработать собственное решение и реализовать в нем необходимую функциональность.

На основе API построены некоторые `готовые решения <howtostart/IntegrationOptions.html#id2>`__, которые можно использовать при разработке клиентских приложений.


.. toctree::
	:hidden:
	:maxdepth: 1
	:titlesonly:
	:caption: История изменений

	ReleaseNotes
 
.. toctree::
	:maxdepth: 1
	:titlesonly:
	:caption: С чего начать

	howtostart/IntegrationOptions
	DataModel
	Overview
   
.. toctree::
	:maxdepth: 1
	:titlesonly:
	:caption: Общее описание возможностей

	Authorization
	DataStructures
	ApiClientOperationPrinciple
	Counteragents
	MiscellaneousApiFeatures

.. toctree::
	:maxdepth: 1
	:titlesonly:
	:caption: Документооборот

	docflows/AttachmentVersion
	docflows/InvoiceDocflow
	docflows/Torg12Docflow
	docflows/AktDocflow
	docflows/UtdDocflow
	docflows/NonformalizedDocflow
	docflows/TemplateDocflow
	docflows/Workflows

.. toctree::
	:maxdepth: 1
	:titlesonly:
	:caption: Примеры использования

	howto/marking_ttgis
	howto/utd820
	howto/example_send_invoice
	howto/example_receive_invoice
	howto/example_torg12
	howto/example_acceptance_certificate
	howto/tags

.. toctree::
	:maxdepth: 1
	:titlesonly:
	:caption: Техническая документация

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
	:caption: Справочная информация

	http_methods
	protos
	obsolete_methods
