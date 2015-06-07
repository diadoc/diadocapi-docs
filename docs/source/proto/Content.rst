Content
=======

.. code-block:: protobuf

    message Content
    {
        required sfixed32 Size = 1;
        optional bytes Data = 2;
    }

Структура представляет содержимое некоторого документа.

-  *Size* - количество байтов в файле документа. Равно -1, если это значение неизвестно.
-  *Data* - байты содержимого.
