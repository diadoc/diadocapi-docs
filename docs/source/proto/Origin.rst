Origin
======

Контракт, описывающий происхождение :doc:`документа <Document>`.

Описание:

.. code-block:: protobuf

    message Origin {
        required MessageType MessageType = 1;
        required string MessageId = 2;
    }

    enum MessageType {
        Unknown = 0;
        Message = 1;
        Draft = 2;
        Template = 3;
    }	

- *MessageType* отражает тип документа, из которого был создан искомый документ. 

    - флаг *Draft* - документ создан из черновика;

    - флаг *Template* - документ создан из шаблона;

    - *Unknown* и *Message* пока не используются, сделаны для будущих возможных сценариев.

- *MessageId* - идентификатор исходной сущности (например, черновика или шаблона соответственно).

.. note::
   В C++ SDK, ввиду особенностей Protobuf, значения в *MessageType* называются *MessageLetter*, *DraftLetter* и *TemplateLetter* соответственно.