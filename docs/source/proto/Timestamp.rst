Timestamp
=========

.. code-block:: protobuf

    message Timestamp
    {
        required sfixed64 Ticks = 1;
    }

Структура представляет некоторый момент времени, не привязанный к часовому поясу. Его можно воспринимать как UTC-время.

-  *Ticks* - целое число тиков (100-наносекундных интервалов), прошедших с момента времени 00:00:00 01.01.0001.

Пример использования (C#)
^^^^^^^^^^^^^^^^^^^^^^^^^

Преобразование в DateTime:

.. code-block:: csharp

    var dt = new DateTime(timestamp.Ticks, DateTimeKind.Utc);
