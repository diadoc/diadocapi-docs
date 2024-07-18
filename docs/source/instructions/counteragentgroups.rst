Группы контрагентов
===================

.. contents:: :local:

Контрагентов, с которыми установлены партнерские отношения, можно распределять по группам.

По умолчанию все контрагенты в группе могут отправлять документы в любое подразделение организации. Но вы можете указать для каждой группы контрагентов, в какие подразделения смогут отправлять документы контрагенты из этой группы. Это может быть полезно в случае, если разные подразделения организации работают с документами от разных контрагентов. 


Создание группы контрагентов
----------------------------

Чтобы создать группу контрагентов, администратор ящика должен выполнить следующие действия:

	#. С помощью метода :doc:`../http/CreateCounteragentGroup` создать группу и указать, в какие подразделения контрагенты группы смогут отправлять документы. В ответе метод вернет информацию о созданной группе.
	#. С помощью метода :doc:`../http/AddCounteragentToGroup` добавить контрагентов в созданную группу. Вызвать метод нужно для каждого контрагента, которого вы хотите добавить в группу.

**Пример HTTP-запроса метода CreateCounteragentGroup:**

.. code-block:: http

	POST /CreateCounteragentGroup?boxId={{boxId}} HTTP/1.1
	Host: diadoc-api.kontur.ru
	Authorization: DiadocAuth ddauth_api_client_id={{apiKey}}, ddauth_token={{token}}
	Accept: application/json; charset=utf-8

**Пример тела запроса метода CreateCounteragentGroup:**

.. code-block:: json

    {
        "Name": "Группа",
        "Departments": {
            "DepartmentIds": [
                "6d710055-9b5d-4bc0-ba2f-9e54adda034e"
            ]
        }
    }

**Пример ответа метода CreateCounteragentGroup:**

.. code-block:: json

    {
        "CounteragentGroupId": "ecd591dd-b56f-4178-ab4a-8a5532f231f7",
        "Name": "Группа",
        "Departments": {
            "DepartmentIds": [
                "6d710055-9b5d-4bc0-ba2f-9e54adda034e"
            ]
        }
    }

**Пример HTTP-запроса метода AddCounteragentToGroup:**

.. code-block:: http

	POST /AddCounteragentToGroup?boxId={{boxId}}&counteragentGroupId=ecd591dd-b56f-4178-ab4a-8a5532f231f7&counteragentBoxId={{counteragentBoxId}} HTTP/1.1
	Host: diadoc-api.kontur.ru
	Authorization: DiadocAuth ddauth_api_client_id={{apiKey}}, ddauth_token={{token}}


Получение списка групп контрагентов
-----------------------------------

Чтобы отредактировать, удалить или получить информацию о конкретной группе, нужно получить ее идентификатор ``CounteragentGroupId``. Это можно сделать с помощью метода ``GetCounteragentGroups``. Метод возвращает идентификатор группы, название и список подразделений, в которое контрагенты группы могут отправлять документы.

**Пример HTTP-запроса метода GetCounteragentGroups:**

.. code-block:: http

    GET /GetCounteragentGroups?boxId={{boxId}} HTTP/1.1
    Host: diadoc-api.kontur.ru
    Authorization: DiadocAuth ddauth_api_client_id={{apiKey}}, ddauth_token={{token}}

**Пример ответа метода GetCounteragentGroups:**

.. code-block:: json

    {
        "Groups": [
            {
                "CounteragentGroupId": "00000000-0000-0000-0000-000000000000",
                "Name": "По умолчанию"
            },
            {
                "CounteragentGroupId": "df6218d0-59bd-44ad-8d56-6e4bfe5fdd2b",
                "Name": "Группа"
            },
            {
                "CounteragentGroupId": "982e047f-bc5c-44e4-a24b-d1ba93f2fd6f",
                "Name": "Новая группа 3",
                "Departments": {
                    "DepartmentIds": [
                        "16703d96-93a5-43a8-b2b6-c9c2f5b89451"
                    ]
                }
            },
            {
                "CounteragentGroupId": "2691abaa-a8ec-4fd5-b2d3-894b434e9643",
                "Name": "Новая группа 4",
                "Departments": {
                    "DepartmentIds": [
                        "1da985dd-611f-4b2c-8938-211943f0706e"
                    ]
                }
            }
        ],
        "TotalCount": 4
    }

Редактирование группы контрагентов
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

С помощью метода :doc:`../http/UpdateCounteragentGroup` можно изменить название группы и список подразделений, в которое контрагенты группы могут отправлять документы.

**Пример HTTP-запроса метода UpdateCounteragentGroup:**

.. code-block:: http

    POST /UpdateCounteragentGroup?boxId={{boxId}}&counteragentGroupId=35263ada-3620-4225-86e6-9a4bd1797fdc HTTP/1.1
    Host: diadoc-api.kontur.ru
    Authorization: DiadocAuth ddauth_api_client_id={{apiKey}}, ddauth_token={{token}}

**Пример тела запроса метода UpdateCounteragentGroup:**

.. code-block:: json

    {
        "Name": "Группа22",
        "GroupDepartment": [
            {
                "DepartmentId": "16703d96-93a5-43a8-b2b6-c9c2f5b89451"
            }
        ]
    }

Получение списка контрагентов группы
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

При удалении группы, всем контрагентам из нее назначается группа «по умолчанию»: контрагенты смогут отправлять документы в любое подразделение организации. Чтобы проверить, какие контрагенты состоят в группе и, при необходимости, добавить их в новую, используйте метод ``GetCounteragentsFromGroup``.

**Пример HTTP-запроса метода GetCounteragentsFromGroup:**

.. code-block:: http

    GET /GetCounteragentsFromGroup?boxId={{boxId}}&counteragentGroupId=2691abaa-a8ec-4fd5-b2d3-894b434e9643 HTTP/1.1
    Host: diadoc-api.kontur.ru
    Authorization: DiadocAuth ddauth_api_client_id={{apiKey}}, ddauth_token={{token}}

**Пример тела ответа метода GetCounteragentsFromGroup:**

.. code-block:: json

    {
        "CounteragentBoxId": [
            "63ea3407-215c-46ba-99f8-9d8e600233e7"
        ],
        "TotalCount": 1,
        "AfterIndexKey": "08D5F86E341FB6DE0734EA635C21BA4699F89D8E600233E7"
    }


** группа по умолчанию **

----

.. rubric:: См. также

*Определение:*
	- :doc:`../entities/counteragent`

*Методы для работы с группами контрагентов:*
	- :doc:`../http/AddCounteragentToGroup` — добавляет контрагентов в группу
	- :doc:`../http/CreateCounteragentGroup` — создает группу контрагентов

	- :doc:`../http/UpdateCounteragentGroup` — редактирует группу контрагентов
	- :doc:`../http/DeleteCounteragentGroup` — удаляет группу контрагентов
	- :doc:`../http/GetCounteragentGroups` — возвращает список групп контрагентов
	- :doc:`../http/GetCounteragentGroup` — возвращает информацию о группе контрагентов
	- :doc:`../http/GetCounteragentsFromGroup` — возвращает список контрагентов в группе

*Структуры для работы с группами контрагентов:*
	- :doc:`../proto/CounteragentGroup` — хранит информацию о группе контрагентов
	- :doc:`../proto/DepartmentsInGroup` — хранит список идентификаторов подразделений, в которые группа контрагентов может отправлять документы
