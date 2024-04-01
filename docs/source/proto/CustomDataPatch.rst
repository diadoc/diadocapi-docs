CustomDataPatch
===============

Структура ``CustomDataPatch`` хранит данные для операции изменения :doc:`тегов <../entities/tag>`.

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

- ``ParentEntityId`` — идентификатор документа, для которого нужно добавить или изменить тег.
- ``Operation`` — тип операции. Принимает значения из перечисления ``CustomDataPatchOperation``:

	- ``Set`` — добавить новый тег или изменить уже существующий.
	- ``Remove`` — удалить тег, если он есть. Значение поля ``Value`` в этой операции игнорируется.
   
- ``Key`` — название тега. Не может быть пустым. Регистронезависимый. Может содержать только буквы латинского и русского алфавита, цифры и символы «-» и «_». Длина не может превышать 60 символов.
- ``Value`` — значение тега, соответствующее ключу ``Key``. Может быть пустым. Регистронезависимый. Длина не может превышать 200 символа. Значение игнорируется, если тип операции — ``Remove``.

----

.. rubric:: См. также

*Руководства:*
	- :doc:`../entities/tag`

*Структура используется:*
	- в структуре :doc:`MessagePatchToPost`.