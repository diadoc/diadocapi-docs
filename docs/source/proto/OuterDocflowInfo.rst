OuterDocflowInfo
================

Структура ``OuterDocflowInfo`` содержит информацию о внешнем документообороте по документу или аннулированию: например, о статусе обработки документа с маркированными товарами в ГИС МТ «Честный ЗНАК».

.. code-block:: protobuf

    message OuterDocflowInfo {
        required string DocflowNamedId = 1;
        required string DocflowFriendlyName = 2;
        required Status Status = 3;
    }
  
    message Status {
        required string NamedId = 1;
        required string FriendlyName = 2;
        required OuterStatusType Type = 3;
        optional string Description = 4;
        repeated StatusDetail Details = 5;
    }

    message StatusDetail {
        optional string Code = 1;
        optional string Text = 2;
    }

.. _OuterStatusType:

.. code-block:: protobuf

    enum OuterStatusType {
        UnknownStatus = 0;
        Normal = 1;
        Success = 2;
        Warning = 3;
        Error = 4;
    }
  
- ``DocflowNamedId`` — именованный идентификатор внешнего документооборота.
- ``DocflowFriendlyName`` — наименование внешнего документооборота; используется для отображения в веб-интерфейсе.
- ``Status`` — информация о статусе обработки документа в рамках документооборота, представленная структурой ``Status`` с полями:

	- ``NamedId`` — именованный идентификатор статуса.
	- ``FriendlyName`` — наименование статуса; используется для отображения в веб-интерфейсе.
	- ``Type`` - тип статуса, полученного в рамках внешнего документооборота. Принимает значения из перечисления ``OuterStatusType``:
	
		- ``UnknownType`` — зарезервировано для устаревших клиентов.
		- ``Normal`` — нормальный. Обычно такой тип присваивается промежуточним статусам, которые не требуют внимания пользователя, например "Обрабатывается в ГИС МТ "Честный ЗНАК".
		- ``Success`` — успешный статус. Соответствует успешному завершению обработки документа.
		- ``Warning`` — предупреждение. Обычно такой тип присваивается промежуточным статусам, на которые требуется обратить внимание пользователя.
		- ``Error`` — ошибка. Соответствует ситуациям, когда в процессе внешнего документооборота возникла ошибка.
	
	- ``Description`` — описание статуса. 
	- ``Details`` — детализация по статусу; может содержать быть список ошибок, которые были получены при взаимодействии с внешним сервисом в рамках документооборота. Преставлена структурой ``StatusDetail`` с полями:
	
		- ``Code`` — код ошибки,
		- ``Text`` — текст ошибки.