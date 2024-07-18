GetDocflowBatchResponse
=======================

.. warning::
	Структура устарела. Вместо нее используется структура :doc:`../GetDocflowBatchResponseV3`.

Структура ``GetDocflowBatchResponse`` представляет собой список документов с информацией о документообороте по каждому из них, полученных методом :doc:`../../http/obsolete/GetDocflows`.

.. code-block:: protobuf

   message GetDocflowBatchResponse
   {
       repeated DocumentWithDocflow Documents = 1;
   }

- ``Documents`` — список документов, представленных структурой :doc:`DocumentWithDocflow`.

----

.. rubric:: См. также

*Структура используется:*
	- в теле ответа метода :doc:`../../http/obsolete/GetDocflows`