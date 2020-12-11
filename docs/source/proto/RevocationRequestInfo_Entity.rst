RevocationRequestInfo
=====================

.. code-block:: protobuf

    message RevocationRequestInfo {
    required string InitiatorBoxId  = 1;
  }
  
Структура данных *RevocationRequestInfo* содержит информацию о соглашении об аннулировании:

-  *InitiatorBoxId* - идентификатор ящика, запросившего аннулирование.
