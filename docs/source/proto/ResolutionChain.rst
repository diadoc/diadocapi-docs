ResolutionChain
===============

.. code-block:: protobuf

    message ResolutionChainList {
        repeated ResolutionChain ResolutionChains = 1;
    }

    message ResolutionChain {
        required string ChainId = 1;
        required string Name = 2;
    }

Структура данных *ResolutionChain* представляет одну цепочку согласования в организации:

-  *ChainId* - уникальный идентификатор цепочки согласования

-  *Name* - имя цепочки согласования
