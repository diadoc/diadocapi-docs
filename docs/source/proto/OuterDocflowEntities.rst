OuterDocflowEntities
================

.. warning:: Эта версия контракта — экспериментальная и может измениться.


.. code-block:: protobuf

    message OuterDocflowEntities
    {	
      required string DocflowNamedId = 1;
      required string DocflowFriendlyName = 2;
      repeated StatusEntity StatusEntities = 3;
    }
    
    message StatusEntity
    {
      required SignedAttachmentV3 Attachment = 1;
      required Status Status = 2;
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
   
В структуре *OuterDocflowEntities* собраны сущности, относящиеся к внешнему документообороту по документу или запросу на аннулирование.
 
-  *DocflowNamedId* - именованный идентификатор внешнего документооборота.
-  *DocflowFriendlyName* - наименование внешнего документооборота, используется для отображения в веб-интерфейсе.
-  *StatusEntities* - набор статусов, полученных в рамках внешнего документооборота.
-  :doc:`Attachment <SignedAttachmentV3>` - содержит информацию о квитанции, которая была получена в рамках внешнего документооборота.
-  *Status* - информация о статусе обработки документа.
  -  *NamedId* - именованный идентификатор статуса,
  -  *FriendlyName* - наименование статуса, используется для отображения в веб-интерфейсе,
  -  :ref:`Type <OuterStatusType>` - тип статуса,
  -  *Description* - дополнительное описание статуса. 
  -  *Details* - детализация по статусу. Здесь может быть список ошибок, которые были получены в при взаимодействии с внешним сервисом в рамках документооборота:
    -  *Code* - код ошибки,
    -  *Text* - текст ошибки.
