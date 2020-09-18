OuterDocflow
================

.. warning:: Эта версия контракта — экспериментальная и может измениться.

.. code-block:: protobuf

  message OuterDocflow
  {
    required string DocflowNamedId = 1;
    required string ParentEntityId = 2;
    required string OuterDocflowEntityId = 3;
  }

Структура представляет собой информацию о последнем полученном состоянии в рамках внешнего документооборота, например, о статусе обработки документа с маркированными товарами в ГИС МТ "Честный ЗНАК":

-  *DocflowNamedId* - именованный идентификатор внешнего документооборота.
-  *ParentEntityId* - идентификатор сущности, по которой получено последнее состояние в рамках внешнего документооборота (сам документ либо запрос на аннулирование).
-  *OuterDocflowEntityId* - идентификатор последнего полученного состояния в рамках данного внешнего документооборота.

Сущность, на которую ссылается *OuterDocflowEntityId*, следует искать в структуре :doc:`OuterDocflowEntities <OuterDocflowEntitiesV3>`, которая находится, в зависимости от значения ParentEntityId, в структуре :doc:`DocflowV3` или :doc:`RevocationDocflowV3`.
