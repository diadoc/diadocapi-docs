﻿DocumentWorkflow
================

Структура ``DocumentWorkflow`` представляет вид документооборота для конкретной :ref:`версии документа <DocumentVersionV2>`.

Подробно о видах документооборота написано на странице :doc:`../docflows/Workflows`.

.. code-block:: protobuf

    message DocumentWorkflow {
        required int32 Id = 1;
        required bool IsDefault = 2;
    }

- ``Id`` — уникальный числовой идентификатор вида документооборота.
- ``IsDefault`` — признак того, что этот вид документооборота будет использован по умолчанию.

У каждого вида документооборота есть собственный набор свойств, определяющий поведение документа с этим видом документооборота. Эти свойства можно получить с помощью метода :doc:`../http/GetWorkflowsSettings`.
Наборы свойств для каждого вида документооборота описаны в таблице на странице :doc:`../docflows/Workflows`.


----

.. rubric:: См. также

*Структура используется:*
	- в структуре :ref:`DocumentVersionV2`
	- идентификатор ``Id`` используется в структурах :doc:`DocumentAttachment` и :doc:`TemplateDocumentAttachment`.
	- в устаревшей структуре :ref:`DocumentVersion`

*Инструкции:*
	- :doc:`../docflows/Workflows`