DssSignResult
=============

Структура ``DssSignResult`` представляет собой результат подписания файлов сертификатом без носителя.

.. code-block:: protobuf

    message DssSignResult {
        optional DssOperationStatus OperationStatus = 1 [default = Unknown];
        repeated DssFileSigningResult FileSigningResults = 2;
        optional DssConfirmType ConfirmType = 3 [default = ComfirmTypeUnknown];
        optional DssOperator Operator = 4 [default = OperatorUnknown];
        optional string PhoneLastNumbers = 5
    }

    message DssFileSigningResult {
        optional DssFileSigningStatus FileSigningStatus = 1 [default = UnknownSigningStatus];
        optional bytes Signature = 2;
    }

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

    enum DssOperationStatus {
        UnknownSigningStatus = 0;
        SigningCompleted = 1;
        SigningError = 2;
    }

    enum DssComfirmType {
        ComfirmTypeUnknown = -1;
        None = 0;
        Sms = 1;
        MyDss = 2;
        Applet = 3;
        MobileSdk = 4;
    }

    enum DssOperator {
        OperatorUnknown = 0;
        Megafon = 1;
        Kontur = 2
    }

- ``OperationStatus`` — статус операции подписания, принимает значение из перечисления ``DssOperationStatus``:

	- ``Unknown`` — неизвестный статус операции; возвращается, если клиент использует устаревшую версию SDK и не может интерпретировать статус операции, переданный сервером;
	- ``InProgress`` — операция выполняется или ожидает подтверждения от владельца сертификата без носителя;
	- ``Completed`` — операция успешно завершена;
	- ``CanceledByUser`` — владелец сертификата без носителя отклонил запрос на подтверждение;
	- ``Timeout`` — владелец сертификата без носителя не подтвердил операцию за отведенный промежуток времени;
	- ``Crashed`` — произошел сбой при выполнении операции;
	- ``UserHasUnconfirmedOperation`` — у владельца сертификата без носителя есть другая неподтвержденная операция; нужно подтвердить или отклонить ее и повторить запрос;
	- ``OperationRetryRequired`` — нужно повторить операцию через 5 минут.

- ``FileSigningResults`` — список результатов подписания каждого файла, представленных структурой ``DssFileSigningResult`` с полями:

	- ``FileSigningStatus`` — статус подписания файла, принимает значение из перечисления ``DssFileSigningStatus``:

		- ``UnknownSigningStatus`` — неизвестный статус; возвращается, если клиент использует устаревшую версию SDK и не может интерпретировать статус, переданный сервером;
		- ``SigningCompleted`` — файл подписан;
		- ``SigningError`` — произошел сбой при подписании файла.

	- ``Signature`` — подпись в формате :rfc:`CMS SignedData <5652#section-5>` в `DER <http://www.itu.int/ITU-T/studygroups/com17/languages/X.690-0207.pdf>`__-кодировке.

- ``ConfirmType`` — способ подтверждения, принимает значение из перечисления ``DssConfirmType``: 

	- ``ComfirmTypeUnknown`` — неизвестный статус; возвращается, если клиент использует устаревшую версию SDK и не может интерпретировать статус, переданный сервером;
	- ``None`` — неизвестный способ подтверждения;
	- ``Sms`` — подтверждение с помощью SMS-сообщения;
	- ``MyDss`` — подтверждение через мобильное приложение;
	- ``Applet`` — подтверждение с помощью Applet на SIM-карте; значение возвращается для МЭПов;
	- ``MobileSdk`` — подтверждение операции через мобильное приложение Контур.Подпись.

- ``DssOperator`` — оператор сертификата без носителя, принимает значение из перечисления:

	- ``OperatorUnknown`` — неизвестный оператор; возвращается, если клиент использует устаревшую версию SDK и не может интерпретировать оператора, переданного сервером;
	- ``Megafon`` — оператор "Мегафон";
	- ``Kontur`` — оператор "СКБ Контур".

- ``PhoneLastNumbers`` — четыре последние цифры номера телефона, используемого для подтверждения.


----

.. rubric:: См. также

*Структура используется:*
	- в теле запроса метода :doc:`../http/DssSignResult`