DocumentDateAndNumber
=====================

.. code-block:: protobuf

    message DocumentDateAndNumber
    {
        optional string DocumentDate = 1;
        optional string DocumentNumber = 2;
    }

Структура представляет дату и номер документа. У формализованных документов (XML) эти поля хранятся в самом файле, у полуформализованных документов они указываются пользователем при отправке.

-  *DocumentDate* - дата документа.
-  *DocumentNumber* - номер документа.
