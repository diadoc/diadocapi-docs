DocumentWorkflow
================

Структура ``DocumentWorkflow`` представляет вид документооборота (workflow) для версии документа :ref:`DocumentVersionV2 <document-version2>`.

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

.. rubric:: Использование

Структура ``DocumentWorkflow`` используется внутри структуры :ref:`DocumentVersionV2 <document-version2>`.