DocumentTransformation
======================

Структура ``DocumentTransformation`` хранит информацию о документе, который нужно трансформировать из шаблона.

.. code-block:: protobuf

    message DocumentTransformation {
        required string DocumentId = 1;
        optional string CustomDocumentId = 2;
    }

- ``DocumentId`` — идентификатор документа для преобразования из шаблона.
- ``CustomDocumentId`` — идентификатор документа во внешней системе; используется для выстраивания связей между документами внутри отправляемого сообщения. Должен быть уникальным в рамках структуры :doc:`MessageToPost`. После отправки сообщения этот идентификатор можно получить в поле ``CustomDocumentId`` структуры :doc:`Document`.


----

.. rubric:: См. также

*Структура используется:*
	- в структуре :doc:`TemplateTransformationToPost`

*Определение:*
	- :doc:`../entities/template`

*Инструкции:*
	- :doc:`../instructions/template`
