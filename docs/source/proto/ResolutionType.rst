ResolutionType
==============

Перечисление ``ResolutionType`` представляет собой тип действия по согласованию.

.. code-block:: protobuf

    enum ResolutionType {
        UndefinedResolutionType = 0;
        Approve = 1;
        Disapprove = 2;
        UnknownResolutionType = 3;
    }

- ``UndefinedResolutionType`` — отменить последнее согласование текущего пользователя.
- ``Approve`` — согласовать документ.
- ``Disapprove`` — отказать в согласовании документа.
- ``UnknownResolutionType`` — неизвестное состояние. Возвращается в случае, если клиент использует устаревшую версию SDK и не может интерпретировать состояние согласования, переданное сервером.

----

.. rubric:: См. также

*Структура используется:*
	- в структуре :doc:`ResolutionInfo`
	- в структуре :ref:`ResolutionV3`