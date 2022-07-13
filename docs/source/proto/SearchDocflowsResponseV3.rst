SearchDocflowsResponseV3
========================

Структура ``SearchDocflowsResponseV3`` представляет собой результат поиска документов методом :doc:`../http/SearchDocflows_V3`.

.. code-block:: protobuf

   message SearchDocflowsResponseV3
   {
       repeated DocumentWithDocflowV3 Documents = 1;
       optional bool HaveMoreDocuments = 2;
   }

- ``Documents`` — список найденных документов, представленный структурой :doc:`DocumentWithDocflowV3`.
- ``HaveMoreDocuments`` - признак того, что поле ``Documents`` содержит не все найденные документы. Остальные документы можно получить постранично, передавая в метод :doc:`../http/SearchDocflows` индекс первого документа очередной страницы: пример использования приведен в описании метода.

----

.. rubric:: Использование

Структура ``SearchDocflowsResponseV3`` возвращается в теле ответа метода :doc:`../http/SearchDocflows_V3`.