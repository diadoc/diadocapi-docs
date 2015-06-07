DocumentProtocol
================

.. code-block:: protobuf

    message DocumentProtocol {
        required bytes PrintForm = 1;
        required bytes Signature = 2;
    }
        

Структура данных DocumentProtocol содержит печатную форму протокола передачи документа в формате PDF и подпись к ней:

-  *PrintForm* - содержимое печатной формы.

-  *Signature* - байты подписи к печатной форме протокола.