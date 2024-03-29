DocumentDirection
=================

.. code-block:: protobuf

    enum DocumentDirection
    {
        UnknownDocumentDirection = 0;
        Inbound = 1;
        Outbound = 2;
        Internal = 3;
    }

Представляет направление движения документа по отношению к тому ящику, от имени которого был сделан запрос информации о документе.

-  *UnknownDocumentDirection* - зарезервировано для обратной совместимости.
-  *Inbound* - входящий документ.
-  *Outbound* - исходящий документ.
-  *Internal* - внутренний документ.
