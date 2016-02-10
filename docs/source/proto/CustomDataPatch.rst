CustomDataPatch
===============

.. code-block:: protobuf

    message CustomDataPatch {
        required string ParentEntityId = 1;
        required CustomDataPatchOperation Operation = 2;
        required string Key = 3;
        optional string Value = 4;
    }

    enum CustomDataPatchOperation {
        Set = 0;
        Remove = 1;
    }
        

Структура данных *CustomDataPatch* представляет операцию по изменению пользовательских данных, привязанных к документу.

-  *Operation* - тип операции; возможные значения:

   -  *Set* - добавить ключ или изменить уже существующий;
   -  *Remove* - удалить ключ, если он есть. Значение поля *Value* при этом игнорируется.

-  *Key* - произвольный непустой регистронезависимый ключ. Допускаются только буквы латинского алфавита, цифры и символы "-" и "_". Длина ключа не должна превышать 128 символов.

-  *Value* - произвольное регистронезависимое значение (возможно, пустое), соответствующее ключу *Key*. Игнорируется, если тип операции *Remove*. Длина не должна превышать 1024 символа.