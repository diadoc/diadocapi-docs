GetDocflowRequest
=================

.. code-block:: protobuf

   message GetDocflowRequest
   {
       required DocumentId DocumentId = 1;
       optional string LastEventId = 2;
       optional bool InjectEntityContent = 3 [default = false];
   }

Структура представляет запрос на выгрузку одного документа вместе с его документооборотом методом :doc:`../http/GetDocflows`.

-  :doc:`DocumentId` - идентификатор документа.
-  *LastEventId* - идентификатор последнего события, которое нужно учесть при формировании результата. Сервер вычисляет состояние документа по цепочке событий, которые с ним происходили. Данный параметр позволяет ограничить эту цепочку некоторым событием.
-  *InjectEntityContent* - признак того, что в выдачу нужно включить содержимое документа.
