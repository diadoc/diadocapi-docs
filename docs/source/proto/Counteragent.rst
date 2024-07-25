Counteragent
============

Структура ``Counteragent`` хранит информацию о контрагенте.

.. code-block:: protobuf

    message Counteragent {
        optional string IndexKey = 1;
        required Organization Organization = 2;
        optional CounteragentStatus CurrentStatus = 3 [default = UnknownCounteragentStatus];
        required sfixed64 LastEventTimestampTicks = 4;
        optional string MessageFromCounteragent = 6;
        optional string MessageToCounteragent = 7;
        optional DocumentId InvitationDocumentId = 8;
        optional string CounteragentGroupId = 9;
    }

- ``IndexKey`` — уникальный ключ контрагента, который можно передавать в метод :doc:`../http/GetCounteragents` в качестве параметра ``afterIndexKey`` для итерирования по всему отфильтрованному списку.

- ``Organization`` — информация об организации-контрагенте, представленная структурой :doc:`Organization`.

- ``CurrentStatus`` — текущий статус отношения партнерства с контрагентом. Может меняться со временем. Принимает значения из перечисления :doc:`CounteragentStatus`.

- ``LastEventTimestampTicks`` — время последнего события из истории взаимодействия с контрагентом, представляет собой целое число тиков, прошедших с момента времени 00:00:00 01.01.0001.

- ``MessageFromCounteragent`` — текст последнего комментария, полученного от контрагента.

- ``MessageToCounteragent`` — текст последнего комментария, отправленного контрагенту.

- ``InvitationDocumentId`` — идентификатор документа, отправленного вместе с приглашением. Представлен структурой :doc:`DocumentId`. Поле заполняется независимо от наличия доступа к документу. Возвращается, если статус контрагента принимает одно из следующих значений:

	- ``CounteragentStatus = IsMyCounteragent``,
	- ``CounteragentStatus = InvitesMe``,
	- ``CounteragentStatus = IsInvitedByMe``.

	Список статусов, для которых возвращается документ, может быть расширен в будущем. 

- ``CounteragentGroupId`` — идентификатор группы, в которую добавлен контрагент. Возвращается, если статус контрагента ``CounteragentStatus = IsMyCounteragent``. Инструкция по работе с группами контрагентов приведена  на странице :doc:`../instructions/counteragentgroups`.


----

.. rubric:: См. также

*Структура используется:*
	- в структуре ``CounteragentList``, возвращаемой методом :doc:`../http/GetCounteragents`
	- в теле ответа метода :doc:`../http/GetCounteragent`

*Определение:*
	- :doc:`../entities/counteragent`

*Инструкции:*
	- :doc:`../instructions/counteragents`
	- :doc:`../instructions/counteragentgroups`

