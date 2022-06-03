Content
=======

Структура ``Content`` представляет содержимое документа.

.. code-block:: protobuf

    message Content
    {
        required sfixed32 Size = 1;
        optional bytes Data = 2;
    }

- ``Size`` — размер содержимого в байтах. Равно -1, если это значение неизвестно.
- ``Data`` — массив байтов содержимого.
