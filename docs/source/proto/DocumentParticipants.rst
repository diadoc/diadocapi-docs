DocumentParticipants
====================

.. code-block:: protobuf

    message DocumentParticipants
    {
        required DocumentParticipant Sender = 1;
        optional DocumentParticipant Proxy = 2;
        optional DocumentParticipant Recipient = 3;
        required bool IsInternal = 4;
    }

    message DocumentParticipant
    {
        required string BoxId = 1;
        optional string DepartmentId = 2;
    }

Структура *DocumentParticipants* содержит информацию об участниках документооборота.

- :ref:`Sender <document-participant>` - отправитель
- :ref:`Proxy <document-participant>` - промежуточный получатель
- :ref:`Recipient <document-participant>` - получатель
- *IsInternal* - является ли документ внутренним

.. _document-participant:

Структура *DocumentParticipant* содержит информацию об участнике документооборота.

- *BoxId* - идентификатор ящика
- *DepartmentId* - идентификатор подразделения
