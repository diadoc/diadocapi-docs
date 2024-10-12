DocumentParticipants
====================

Структура ``DocumentParticipants`` хранит информацию об участниках документооборота.

.. code-block:: protobuf

    message DocumentParticipants
    {
        required DocumentParticipant Sender = 1;
        optional DocumentParticipant Proxy = 2;
        optional DocumentParticipant Recipient = 3;
        required bool IsInternal = 4;
    }



- ``Sender`` — отправитель документа, представленный структурой :ref:`DocumentParticipant`.
- ``Proxy`` — промежуточный получатель документа, представленный структурой :ref:`DocumentParticipant`.
- ``Recipient`` — получатель документа, представленный структурой :ref:`DocumentParticipant`.
- ``IsInternal`` — признак того, что документ является внутренним.


.. _DocumentParticipant:

DocumentParticipant
-------------------

Структура ``DocumentParticipant`` хранит информацию об участнике документооборота.

.. code-block:: protobuf

    message DocumentParticipant
    {
        required string BoxId = 1;
        optional string DepartmentId = 2;
    }

- ``BoxId`` — идентификатор ящика.
- ``DepartmentId`` — идентификатор подразделения.


----

.. rubric:: См. также

*Структура используется:*
	- в структуре :doc:`DocumentInfoV3`
	- в структуре :doc:`DocumentTemplateInfo <DocumentInfoV3>`