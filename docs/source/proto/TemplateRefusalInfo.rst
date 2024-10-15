TemplateRefusalInfo
===================

.. code-block:: protobuf

    message TemplateRefusalInfo {
        required TemplateRefusalType Type = 1 [default = UnknownTemplateRefusalType];
        required string BoxId = 2;
        optional string Author = 3;
        optional string Comment = 4;
    }

Структура содержит информацию об отзыве или отклонении шаблона. Содержится в структуре :doc:`Entity`.

- :ref:`Type <TemplateRefusalType>` - тип действия (отклонение или отзыв).
- *BoxId* - идентификатор ящика, на стороне которого выполнено действие.
- *Author* - ФИО пользователя, который выполнил действие.
- *Comment* - комментарий, который был указан при отклонении/отзыве. Длина не более 2000 символов.

.. _TemplateRefusalType:

TemplateRefusalType
-------------------

.. code-block:: protobuf

    enum TemplateRefusalType {
        UnknownRefusalType = 0;
        Refusal = 1;
        Withdrawal = 2;
    }

Перечисление отражает тип отказа по шаблону:

- *UnknownRefusalType* - зарезервировано для устаревших клиентов.
- *Refusal* - отклонение.
- *Withdrawal* - отзыв.