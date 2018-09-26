Origin
======

Контракт, описывающий происхождение :doc:`документа <Document>`.

.. code-block:: protobuf

    message Origin {
        required MessageType MessageType = 1;
        required string MessageId = 2;
    }

    enum MessageType {
        Unknown = 0;
        Letter = 1;
        Draft = 2;
        Template = 3;
    }	

- *MessageType* отражает тип документа, из которого был создан искомый документ. 

    - флаг *Draft* - документ создан из черновика;

    - флаг *Template* - документ создан из шаблона;

    - флаг *Letter* пока не используется, создан для будущих возможных сценариев.

- *MessageId* - идентификатор исходной сущности (например, черновика или шаблона соответственно).

.. note::
   В C++ SDK, ввиду особенностей Protobuf, значения в *MessageType* называются *MessageLetter*, *DraftLetter* и *TemplateLetter* соответственно.
