DocflowStatus
=============

.. code-block:: protobuf

   message DocflowStatus
   {
       optional DocflowStatusModel PrimaryStatus = 1;
       optional DocflowStatusModel SecondaryStatus = 2;
   }

Структура представляет информацию о статусе документооборота. 

Статус формируется с точки зрения пользователя, от имени которого был сделан запрос на получение этой информации.

-  :doc:`PrimaryStatus <DocflowStatusModel>` - основная компонента статуса.

-  :doc:`SecondaryStatus <DocflowStatusModel>` - второстепенная компонента статуса.
