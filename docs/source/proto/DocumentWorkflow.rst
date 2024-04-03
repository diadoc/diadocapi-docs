DocumentWorkflow
================

Структура ``DocumentWorkflow`` представляет вид документооборота для версии документа :ref:`DocumentVersionV2 <document-version2>`.

Подробно о видах документооборота написано на странице :doc:`../docflows/Workflows`.

.. code-block:: protobuf

    message DocumentWorkflow {
        required int32 Id = 1;
        required bool IsDefault = 2;
    }

- ``Id`` — уникальный числовой идентификатор вида документооборота.
- ``IsDefault`` — признак того, что этот вид документооборота будет использован по умолчанию.

У каждого вида документооборота есть собственный набор свойств, определяющий поведение документа с этим видом документооборота. Эти свойства можно получить с помощью метода :doc:`../http/GetWorkflowsSettings`.
Наборы свойств для каждого вида документооборота описаны в таблице на странице :doc:`DocumentWorkflowSettings`.

----

.. rubric:: См. также

*Структура используется:*
	- в структуре :ref:`DocumentVersionV2 <document-version2>`.
	
*Руководства:*
	- :doc:`../docflows/Workflows`