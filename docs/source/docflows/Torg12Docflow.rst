.. _torg12-docflow:

Документооборот накладных
=========================

Процесс обмена электронными накладными в Диадоке реализован с учетом `Приказа ФНС России от 21 марта 2012 № ММВ-7-6/172@ <https://normativ.kontur.ru/document?moduleId=1&documentId=261859>`__.

.. seealso::
    Подробнее про электронные накладные можно прочитать `здесь <http://www.diadoc.ru/docs/others/tn>`__

.. note::
    Порядок обмена электронными накладными между компаниями через Диадок описан `здесь <https://wiki.diadoc.ru/pages/viewpage.action?pageId=1147081>`__

Форматы
-------

Электронные накладные в Диадоке можно создавать:

- по формату, утвержденному приказом ФНС `от 21 марта 2012 № ММВ-7-6/172@ <https://normativ.kontur.ru/document?moduleId=1&documentId=261859>`__, с учетом внесенных изменений приказом `от 2 февраля 2015 г. N ММВ-7-15/40@ <https://normativ.kontur.ru/document?moduleId=1&documentId=248109>`__.

В силу приказов `№ ММВ-7-6/172@ <https://normativ.kontur.ru/document?moduleId=1&documentId=261859>`__ и `N ММВ-7-15/40@ <https://normativ.kontur.ru/document?moduleId=1&documentId=248109>`__ электронная товарная накладная может быть в следующем формате:

-  :download:`XSD-схема титула продавца электронной накладной <../xsd/DP_OTORG12_1_986_00_05_01_02.xsd>`; 

-  :download:`XSD-схема титула покупателя электронной накладной <../xsd/DP_PDOTPR_1_983_00_01_01_02.xsd>`; 


Структуры
---------

Для документов, возникающих в ходе документооборота электронных накладных, в Диадоке зарезервированы специальные :doc:`типы сущностей <../proto/Entity message>`.

Для титула продавца электронной накладной можно использовать следующий структуры:

-  *Attachment/XmlTorg12* (приказ `№ ММВ-7-6/172@ <https://normativ.kontur.ru/document?moduleId=1&documentId=249567>`__),

-  *Attachment/UniversalTransferDocument* (УПД с функцией ДОП, *FunctionType.Basic*, `приказ N ММВ-7-15/155@ <https://normativ.kontur.ru/document?moduleId=1&documentId=271958>`__),

Для титула покупателя электронной накладной можно использовать следующий структуры:

-  *Attachment/XmlTorg12BuyerTitle* (приказ `№ ММВ-7-6/172@ <https://normativ.kontur.ru/document?moduleId=1&documentId=249567>`__),

-  *Attachment/UniversalTransferDocumentRevision* (исправление УПД с функцией ДОП, *FunctionType.Basic*, `приказ N ММВ-7-15/155@ <https://normativ.kontur.ru/document?moduleId=1&documentId=271958>`__),


Порядок обмена
--------------
