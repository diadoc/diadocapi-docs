OuterDocflowInfo
================
.. code-block:: protobuf

  message OuterDocflowInfo {
      required string DocflowNamedId = 1;
      required string DocflowFriendlyName = 2;
      required Status Status = 3;
  }
  
  message Status {
      required string NamedId = 1;
      required string FriendlyName = 2;
      required StatusType Type = 3;
      optional string Description = 4;
      repeated StatusDetail Details = 5;	
  }
  
  message StatusDetail{
      optional string Code = 1;
      optional string Text = 2;
  }
  
Структура *OuterDocflowInfo* содержит информацию о внешнем документообороте по документу/аннулированию, например, о статусе обработки документа с маркированными товарами в ГИС МТ "Честный ЗНАК":

-  *DocflowNamedId* - именованный идентификатор внешнего документооборота.
-  *DocflowFriendlyName* - наименование внешнего документооборота, используется для отображения в веб-интерфейсе.
-  *Status* - информация о статусе обработки документа в рамках документооборота
  -  *NamedId* - именованный идентификатор статуса,
  -  *FriendlyName* - наименование статуса, используется для отображения в веб-интерфейсе,
  -  :ref:`Type <OuterStatusType>` - тип статуса,
  -  *Description* - дополнительное описание статуса. 
  -  *Details* - детализация по статусу. Здесь может быть список ошибок, которые были получены при взаимодействии с внешним сервисом в рамках документооборота
    -  *Code* - код ошибки,
    -  *Text* - текст ошибки.
  
.. _OuterStatusType:

OuterStatusType
-------------------

.. code-block:: protobuf

  enum OuterStatusType{
      UnknownType = 0;
      Normal = 1;
      Success = 2;
      Warning = 3;
      Error = 4;
  }
  
Перечисление отражает тип статуса, полученного в рамках внешнего документооборота:

-  *UnknownType* - зарезервировано для устаревших клиентов.
-  *Normal* - нормальный. Обычно такой тип присваивается промежуточним статусам, которые не требуют внимания пользователя, например "Обрабатывается в ГИС МТ "Честный ЗНАК".
-  *Success* - успешный статус. Соответствует успешному завершению обработки документа.
-  *Warning* - предупреждение. Обычно такой тип присваивается промежуточным статусам, на которые требуется обратить внимание пользователя.
-  *Error* - ошибка. Соответствует ситуациям, когда в процессе внешнего документооборота возникла ошибка.
