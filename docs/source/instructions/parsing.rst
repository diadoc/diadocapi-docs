Парсинг формализованного документа
==================================

В некоторых ситуациях может потребоваться «разобрать» титул документа на составляющие элементы и получить их значения: например, когда нужно:

	- перенести данные документа из Диадока в учетную систему пользователя,
	- получить данные предыдущего титула и сгенерировать с их помощью титулы последующих участников,
	- выполнить опереленные действия с документом в зависимости от его содержимого.

Сделать это вручную может быть сложно: XML-файлы документов имеют сложную структуру и зависимости между элементами, которые нужно анализировать при разборе. Например, в качестве продавца в универсальном передаточном документе (УПД) могут быть указаны юридическое лицо (ЮЛ) или индивидуальный предприниматель (ИП). В XML-файле документа однотипные реквизиты (наименование, ИНН и т.д.) для ЮЛ и ИП находятся в разных элементах, но в учетных системах могут храниться в одном объекте.

Поэтому Диадок предоставляет возможность получить данные титула формализованного документа уже в готовом виде. Сделать это можно следующими способами:

	- если документ хранится в Диадоке, то можно взять данные из структуры титула, полученного с помощью методов

		- :doc:`../http/GetMessage`,
		- :doc:`../http/GetDocument`,
		- :doc:`../http/GetDocflows_V3`,

	- если документ имеется в виде XML-файла, то можно выполнить его парсинг, чтобы работать с упрощенным XML-файлом UserDataXml.

Парсинг документа и формирование упрощенного XML-файла титула выполняется с помощью метода :doc:`../http/ParseTitleXml`. Чтобы распарсить документ, нужно знать его тип, функцию, версию и номер титула. Узнать эти данные можно следующими способами:

	- из ответов методов

		- :doc:`../http/GetNewEvents`,
		- :doc:`../http/GetDocflowEvents_V3`,
		- :doc:`../http/GetDocflows_V3`,
		- :doc:`../http/GetMessage`,
		- :doc:`../http/GetDocument`,

	- с помощью метода детектирования :doc:`../http/DetectDocumentTitles`.

.. image:: ../_static/img/diadoc-api-parse-xml-schema1.png
	:align: center

В теле запроса метода ``ParseTitleXml`` нужно передать XML-файл титула документа. Метод «разберет» его и вернет упрощенный XML-файл UserDataXml, который вы можете использовать в своем интеграционном решении.

**Пример HTTP-запроса метода ParseTitleXml:**

.. tabs::

	.. tab:: УПД 970

		.. code-block:: http

			POST /ParseTitleXml?boxId={{boxId}}&documentTypeNamedId=UniversalTransferDocument&documentFunction=СЧФДОП&documentVersion=utd970_05_02_01&titleIndex=0 HTTP/1.1
			Host: diadoc-api.kontur.ru
			Authorization: DiadocAuth ddauth_api_client_id={{apiKey}}, ddauth_token={{token}}
			Content-Type: application/xml; charset=utf-8

	.. tab:: УПД 820

		.. code-block:: http

			POST /ParseTitleXml?boxId={{boxId}}&documentTypeNamedId=UniversalTransferDocument&documentFunction=СЧФДОП&documentVersion=utd820_05_01_02_hyphen&titleIndex=0 HTTP/1.1
			Host: diadoc-api.kontur.ru
			Authorization: DiadocAuth ddauth_api_client_id={{apiKey}}, ddauth_token={{token}}
			Content-Type: application/xml; charset=utf-8

**Пример тела запроса метода ParseTitleXml:**

.. tabs::

	.. tab:: УПД 970

		.. container:: toggle

			.. literalinclude:: ../include/generate_utd970_05_02_01_title0_resp.xml
				:encoding: windows-1251

	.. tab:: УПД 820

		.. container:: toggle

			.. literalinclude:: ../include/generate_utd820_05_01_02_hyphen_title0_resp.xml
				:encoding: windows-1251

**Пример тела ответа метода ParseTitleXml:**

.. tabs::

	.. tab:: УПД 970

		.. container:: toggle

			.. literalinclude:: ../include/parse_utd970_05_02_01_title0_resp.xml

	.. tab:: УПД 820

		.. container:: toggle

			.. literalinclude:: ../include/parse_utd820_05_01_02_hyphen_title0_resp.xml

В ответе метод ``ParseTitleXml`` вернет упрощенный XML-файл UserDataXml. После получения упрощенного XML-файла вы можете использовать его в своем интеграционном решении.


----

.. rubric:: См. также

*Инструкции:*
	- :doc:`getdoctypes`
	- :doc:`generation`
	- :doc:`utd`

*Методы для работы с титулами:*
	- :doc:`../http/GenerateTitleXml` — генерирует XML-файл любого титула для любого типа документа
	- :doc:`../http/ParseTitleXml` — парсит XML-файл титула на элементы