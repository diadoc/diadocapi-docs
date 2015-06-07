DocumentsMoveOperation
======================

.. code-block:: protobuf

    message DocumentsMoveOperation
    {
        required string BoxId = 1;
        optional string ToDepartmentId = 2;
        repeated DocumentId DocumentIds = 3;
    }
        

Структура данных DocumentsMoveOperation задает информацию для операции перемещения документов между подразделениями организации.

-  *BoxId* - идентификатор ящика, в котором находятся документы.

-  *ToDepartmentId* - идентификатор подразделения, в которое необходимо переместить документы.

-  *DocumentIds* - список идентификаторов документов, которые необходимо переместить.