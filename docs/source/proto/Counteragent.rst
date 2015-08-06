Counteragent
============

.. code-block:: protobuf

    message CounteragentList {
        required int32 TotalCount = 1;
        repeated Counteragent Counteragents = 2;
    }

    message Counteragent {
        optional string IndexKey = 1;
        required Organization Organization = 2;
        optional CounteragentStatus CurrentStatus = 3 [default = UnknownCounteragentStatus];
        required sfixed64 LastEventTimestampTicks = 4;
        optional string MessageFromCounteragent = 6;
        optional string MessageToCounteragent = 7;
    }

    enum CounteragentStatus {
        UnknownCounteragentStatus = 0;
        IsMyCounteragent = 1;
        InvitesMe = 2;
        IsInvitedByMe = 3;
        RejectsMe = 5;
        IsRejectedByMe = 6;
        NotInCounteragentList = 7;
    }

    message CounteragentCertificateList {
        repeated Certificate Certificates = 1;
    }

    message Certificate {
        required bytes RawCertificateData = 1;
    }
        

Структура данных *CounteragentList* представляет собой список контрагентов *Counteragent*, возвращаемый методом :doc:`../http/GetCounteragents`. Поле *CounteragentList.TotalCount* содержит общее количество контрагентов, удовлетворяющих фильтру.

Структура данных *Counteragent* содержит информацию об одном контрагенте:

-  *IndexKey* - уникальный ключ контрагента, который можно передавать в метод :doc:`../http/GetCounteragents` в качестве параметра afterIndexKey для итерирования по всему отфильтрованному списку.

-  *Organization* - информация об организации-контрагенте, представленная в виде структуры :doc:`Organization`.

-  *CurrentStatus* - текущий статус отношения партнерства с данным контрагентом; может меняться со временем; возможные значения:

   -  *UnknownCounteragentStatus* (неизвестный статус, может выдаваться лишь в случае, когда клиент использует устаревшую версию SDK и не может интерпретировать статус контрагента, переданный сервером),

   -  *IsMyCounteragent* (отношение партнерства установлено и действует),

   -  *InvitesMe* (данный контрагент прислал запрос на установление отношения партнерства),

   -  *IsInvitedByMe* (в адрес данного контрагента был отправлен запрос на установление отношения партнерства),

   -  *RejectsMe* (отношение партнерства было разоварвано со стороны контрагента, либо запрос на установление отношения партнерства был отклонен контрагентом),

   -  *IsRejectedByMe* (отношение партнерства было разоварвано со стороны текущей организации, либо запрос на установление отношения партнерства был отклонен текущей организацией),

   -  *NotInCounteragentList* (специальное значение, выдаваемое для организаций, которые отсутствуют в списке контрагентов текущей организации; не может выдаваться при получении структур Counteragent методами :doc:`../http/GetCounteragent` и :doc:`../http/GetCounteragent`).   

-  *LastEventTimestampTicks* - :doc:`метка времени <Timestamp>` последнего события из истории взаимодействия с данным контрагентом.

-  *MessageFromCounteragent* - текст последнего комментария, полученного от контрагента, из истории взаимодействия ним.

-  *MessageToCounteragent* - текст последнего комментария, отправленного контрагенту, из истории взаимодействия ним.

Структура данных *CounteragentCertificateList* представляет собой список сертификатов контрагента представленных в виде структуры *Certificate*.

Структура *Certificate* представляет собой один сертификат:

-  *RawCertificateData* - сам сертификат, сериализованный в массив байтов в DER-кодировке.