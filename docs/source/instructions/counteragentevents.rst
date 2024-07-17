Лента событий по контрагентам
=============================

.. contents:: :local:

Диадок предоставляет возможность отслеживать события, произошедшие с контрагентами. С помощью этих событий вы можете получать информацию об изменениях, произошедших в отношениях с контрагентом.

Для получения событий по контрагентам используйте метод :doc:`../http/GetCounteragentEvents`. Он вернет в ответе структуру :doc:`../proto/BoxCounteragentEventList`, содержащую информацию о контрагенте, с которым произошло событие, и о самом событии.

Метод возвращает только некоторые типы событий, они указаны в перечислении :doc:`EventTypes <../proto/BoxCounteragentEventList>`.

**Пример HTTP-запроса метода GetCounteragentEvents:**

.. code-block:: http

	GET /V1/GetCounteragentEvents?boxId={{boxId}} HTTP/1.1
	Host: diadoc-api.kontur.ru
	Authorization: DiadocAuth ddauth_api_client_id={{apiKey}}, ddauth_token={{token}}
	Accept: application/json; charset=utf-8

**Пример тела ответа метода GetCounteragentEvents:**

.. code-block:: json

    {
        "Events": [
            {
                "EventId": "765de718-442e-11ef-8007-828b06413688",
                "Counteragent": {
                    "CounteragentBoxId": "09ae254c-5cd0-4082-84de-7ccb46d86f82",
                    "Status": "IsRejectedByMe",
                    "EventTimestampTicks": 638568119816675479,
                    "LastEventComment": "удаление из списка контрагентов",
                    "MessageToCounteragent": "удаление из списка контрагентов"
                },
                "IndexKey": "CNymUlqSJxhMJa4J0FyCQITefMtG2G+C",
                "EventTypes": [
                    "IBrokeUpWithCounteragent"
                ]
            },
            {
                "EventId": "7c313a39-442e-11ef-8010-9fb6f747d48a",
                "Counteragent": {
                    "CounteragentBoxId": "09ae254c-5cd0-4082-84de-7ccb46d86f82",
                    "Status": "IsInvitedByMe",
                    "EventTimestampTicks": 638568119914355510
                },
                "IndexKey": "CNymUmBlejlMJa4J0FyCQITefMtG2G+C",
                "EventTypes": [
                    "IInvitedCounteragent"
                ]
            }
        ],
        "TotalCount": 2,
        "TotalCountType": "Equal"
    }

В указанном выше примере произошло два события:

	#. Событие с идентификатором ``765de718-442e-11ef-8007-828b06413688``:

		- произошло с контрагентом ``09ae254c-5cd0-4082-84de-7ccb46d86f82``. Из блока ``Counteragent``, помимо идентификатора ящика контрагента, можно получить следующую информацию:

			- текущий статус отношений с контрагентом после возникновения события: ``IsRejectedByMe`` — контрагент был удален мной из списка контрагентов;
			- время возникновения события;
			- комментарии по событию.

		- тип произошедшего события: ``EventTypes = IBrokeUpWithCounteragent`` — я разорвал отношения с контрагентом.

	#. Событие с идентификатором ``7c313a39-442e-11ef-8010-9fb6f747d48a``:

		- произошло с контрагентом ``09ae254c-5cd0-4082-84de-7ccb46d86f82``. Из блока ``Counteragent``, помимо идентификатора ящика контрагента, можно получить следующую информацию:

			- текущий статус отношений с контрагентом после возникновения события: ``IsInvitedByMe`` — контрагент приглашен мной;
			- время возникновения события,
			- комментариев по событию нет.

		- тип произошедшего события: ``EventTypes = IInvitedCounteragent`` — я отправил контрагенту приглашение.

Из этого примера можно получить информацию о том, что контрагент ``09ae254c-5cd0-4082-84de-7ccb46d86f82`` сначала был удален из списка контрагентов, а затем вновь приглашен.


----

.. rubric:: См. также

*Определение:*
	- :doc:`../entities/counteragent`

*Методы для работы с событиями по контрагентам:*
	- :doc:`../http/GetCounteragentEvents` — возвращает список событий по изменению отношений с контрагентами

*Структуры для работы с событиями по контрагентам:*
	- :doc:`../proto/BoxCounteragentEventList` — представляет собой список событий по изменению отношений