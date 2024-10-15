SearchDocflowsResponse
======================

.. warning::
	Структура устарела. Вместо нее используется структура :doc:`../SearchDocflowsResponseV3`.

Структура ``SearchDocflowsResponse`` представляет собой результат поиска документов методом :doc:`../../http/obsolete/SearchDocflows_v2`.

.. code-block:: protobuf

   message SearchDocflowsResponse
   {
       repeated DocumentWithDocflow Documents = 1;
       optional bool HaveMoreDocuments = 2;
   }

- ``Documents`` — список найденных документов, представленный структурой :doc:`DocumentWithDocflow`.
- ``HaveMoreDocuments`` - признак того, что поле ``Documents`` содержит не все найденные документы. Остальные документы можно получить постранично, передавая в метод :doc:`../../http/obsolete/SearchDocflows_v2` индекс первого документа очередной страницы: пример использования приведен в описании метода.


----

.. rubric:: См. также

*Структура используется:*
	- в теле ответа устаревшего метода :doc:`../../http/obsolete/SearchDocflows_v2`