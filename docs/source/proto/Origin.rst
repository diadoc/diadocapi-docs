Origin
======

Контракт, описывающий происхождение :doc:`документа <Document>`.

Описание:

.. code-block:: protobuf

    message Origin {
        required LetterType LetterType = 1;
        required string LetterId = 2;
    }

    enum LetterType {
        Unknown = 0;
        Letter = 1;
        Draft = 2;
        Template = 3;
    }	

- *LetterType* отражает тип, из которого был создан документ. 

    - флаг *Draft* - документ создан из черновика;

    - флаг *Template* - документ создан из шаблона;

    - *Unknown* и *Letter* пока не используются, сделаны для будущих возможных сценариев.

- *LetterId* - идентификатор исходной сущности (содержит *MessageId* черновика или шаблона соответственно).