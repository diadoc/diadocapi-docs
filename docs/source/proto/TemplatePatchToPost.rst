TemplatePatchToPost
===================

Структура представляет дополнение к шаблону, подлежащее отправке при помощи метода :doc:`../http/PostTemplatePatch`.

.. code-block:: protobuf

    message TemplatePatchToPost {
        repeated TemplateRefusalAttachment Refusals = 1;
    }

- :ref:`Refusals <TemplateRefusalAttachment>` - список отклонений или отзывов документов шаблона.


.. _TemplateRefusalAttachment:

TemplateRefusalAttachment
-------------------------

.. code-block:: protobuf

    message TemplateRefusalAttachment {
        required string DocumentId = 1;
        optional string Comment = 2; 
        repeated string Labels = 3;
    }

Структура представляет отклонение или отзыв документа из шаблона.

- *DocumentId* - идентификатор документа.
- *Comment* - комментарий к отклонению или отзыву. Длина не более 2000 символов.
- *Labels* - :doc:`метки <../entities/label>` извещения о получении.