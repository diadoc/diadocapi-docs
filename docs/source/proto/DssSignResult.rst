DssSignResult
=============

.. code-block:: protobuf

    message DssSignResult {
        optional DssOperationStatus OperationStatus = 1 [default = Unknown];
        repeated DssFileSigningResult FileSigningResults = 2;
        optional DssConfirmType ConfirmType = 3;
        optional DssOperator Operator = 4;
        optional string PhoneLastNumbers = 5
    }
        

Структура описывает результат подписания файлов сертификатом без носителя. Возвращается методом :doc:`../http/DssSignResult`.

- :ref:`OperationStatus <dss-operation-status>` - статус операции подписания

- :ref:`FileSigningResults <dss-file-signing-result>` - результаты подписания каждого файла

- :ref:`DssConfirmType <dss-confirm-type>` - способ подтверждения

- :ref:`DssOperator <dss-operator>` -  оператор сертификата без носителя

- *PhoneLastNumbers* - четыре последние цифры номера телефона, используемого для подтверждения

.. _dss-operation-status:

DssOperationStatus
------------------

.. code-block:: protobuf

    enum DssOperationStatus {
        Unknown = 0;
        InProgress = 1;
        Completed = 2;
        CanceledByUser = 3;
        Timeout = 4;
        Crashed = 5;
        UserHasUnconfirmedOperation = 6;
        OperationRetryRequired = 7;
    }
    
Описывает состояние операции подписания файлов DSS-сертификатом.

- *Unknown* - неизвестный статус операции. Будет возвращено, если клиент использует устаревшую версию SDK и не может интерпретировать статус операции, возвращенный сервером
- *InProgress* - операция находится в процессе или ожидает подтверждения от владельца сертификата без носителя
- *Completed* - операция успешно завершена
- *CanceledByUser* - владелец сертификата без носителя отклонил запрос на подтверждение
- *Timeout* - владелец сертификата без носителя не подтвердил операцию за отведенный промежуток времени
- *Crashed* - произошел сбой при выполнении операции
- *UserHasUnconfirmedOperation* - у владельца сертификата без носителя есть другая неподтвержденная операция. Необходимо подтвердить или отклонить ее, после чего повторить запрос
- *OperationRetryRequired* - необходимо повторить операцию через 5 минут

.. _dss-file-signing-result:

DssFileSigningResult
--------------------

.. code-block:: protobuf

    message DssFileSigningResult {
        optional DssFileSigningStatus FileSigningStatus = 1 [default = UnknownSigningStatus];
        optional bytes Signature = 2;
    }

Структура описывает результат подписания конкретного файла DSS-сертификатом.

- :ref:`FileSigningStatus <dss-file-signing-status>` - статус подписания файла
- *Signature* - подпись в формате :rfc:`CMS SignedData <5652#section-5>` в `DER <http://www.itu.int/ITU-T/studygroups/com17/languages/X.690-0207.pdf>`__-кодировке


.. _dss-file-signing-status:

DssFileSigningStatus
~~~~~~~~~~~~~~~~~~~~

.. code-block:: protobuf

    enum DssOperationStatus {
        UnknownSigningStatus = 0;
        SigningCompleted = 1;
        SigningError = 2;
    }

Описывает статус подписания конкретного файла сертификата без носителя.

- *UnknownSigningStatus* - неизвестный статус. Будет возвращено, если клиент использует устаревшую версию SDK и не может интерпретировать статус, возвращенный сервером
- *SigningCompleted* - файл подписан
- *SigningError* - произошел сбой при подписании файла

.. _dss-confirm-type:

DssComfirmType
~~~~~~~~~~~~~~
.. code-block:: protobuf

    enum DssComfirmType {
        Unknown = -1;
        None = 0;
        Sms = 1;
        MyDss = 2; 
        Applet = 3;   
    }

Описывает способ подтверждения подписи.

- *Unknown* - неизвестный статус. Будет возвращено, если клиент использует устаревшую версию SDK и не может интерпретировать статус, возвращенный сервером
- *None* - неизвестный способ подтверждения
- *Sms* - подтверждение с помощью SMS-сообщения
- *MyDss* - подтверждение через мобильное приложение. Это означает, что сертификат без носителя
- *Applet* - подтверждение с помощью Applet на SIM-карте. Такое значение возвращается для МЭПов

.. _dss-operator:

DssOperator
~~~~~~~~~~~~~~
.. code-block:: protobuf

    enum DssOperator {
        Unknown = 0;
        Megafon = 1;
        Kontur = 2
    }

- *Unknown* - неизвестный статус. Будет возвращено, если клиент использует устаревшую версию SDK и не может интерпретировать статус, возвращенный сервером
- *Megafon* - оператор "Мегафон"
- *Kontur* - оператор "СКБ Контур"
