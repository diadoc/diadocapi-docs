Content
=======

Структура ``Content`` представляет собой содержимое документа.

.. code-block:: protobuf

    message Content
    {
        required sfixed32 Size = 1;
        optional bytes Data = 2;
    }

- ``Size`` — размер содержимого в байтах. Равно -1, если это значение неизвестно.
- ``Data`` — массив байтов содержимого.


----

.. rubric:: См. также

*Структура используется:*
	- в структуре :doc:`Document`
	- в структуре :doc:`Entity`
	- в структуре :doc:`Entity message`