Entity
======

.. code-block:: protobuf

   message Entity
   {
       optional string EntityId = 1;
       optional Timestamp CreationTimestamp = 2;
       optional Content Content = 3;
   }

Структура представляет информацию о содержимом документа и времени его создания.

-  *EntityId* - идентификатор документа.
-  :doc:`CreationTimestamp <Timestamp>` - время создания документа.
-  :doc:`Content` - содержимое файла документа.
