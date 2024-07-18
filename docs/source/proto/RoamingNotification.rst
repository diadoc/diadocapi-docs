RoamingNotification
===================

Структура ``RoamingNotification`` хранит информацию о статусе доставки документа в роуминг.

.. code-block:: protobuf

    message RoamingNotification
    {
        required Entity Notification = 1;
        required bool IsSuccess = 2;
    }

- ``Notification`` — описание ошибки доставки, представленное структурой :doc:`Entity`. Может отсутствовать.
- ``IsSuccess`` — флаг, означающий успешную доставку документа в роуминг.


----

.. rubric:: См. также

*Структура используется:*
	- в структуре :doc:`RevocationRequestDocflow <RevocationDocflowV3>`
	- в структуре :doc:`SenderTitleDocflow`
	- в устаревшей структуре :doc:`obsolete/Docflow`
