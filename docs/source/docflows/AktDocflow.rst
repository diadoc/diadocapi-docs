.. _akt-docflow:

Документооборот актов
=====================

Процесс обмена электронными актами в Диадоке реализован с учетом `Приказа ФНС России от 21 марта 2012 № ММВ-7-6/172@ <https://normativ.kontur.ru/document?moduleId=1&documentId=261859>`__.

Форматы
-------

Электронные акты в Диадоке можно создавать по формату, утвержденному приказом ФНС `от 21 марта 2012 № ММВ-7-6/172@ <https://normativ.kontur.ru/document?moduleId=1&documentId=261859>`__, с учетом внесенных изменений приказом `от 2 февраля 2015 г. N ММВ-7-15/40@ <https://normativ.kontur.ru/document?moduleId=1&documentId=248109>`__.

В силу приказов `№ ММВ-7-6/172@ <https://normativ.kontur.ru/document?moduleId=1&documentId=261859>`__ и `N ММВ-7-15/40@ <https://normativ.kontur.ru/document?moduleId=1&documentId=248109>`__ электронный акт может быть в следующем формате:

-  :download:`XSD-схема титула исполнителя электронного акта <../xsd/DP_IAKTPRM_1_987_00_05_01_02.xsd>`; 

-  :download:`XSD-схема титула заказчика электронного акта <../xsd/DP_ZAKTPRM_1_990_00_05_01_02.xsd>`;

Также, в силу приказа `N ММВ-7-15/155@ <https://normativ.kontur.ru/document?moduleId=1&documentId=271958>`__, утвержден электронный формат универсального передаточного документа УПД. Его можно использовать как первичный документ, подтверждающий совершение хозяйственной операции; 

-  :download:`XSD-схема формата УПД (с функцикй ДОП) <../xsd/ON_SCHFDOPPR_1_995_01_05_01_01.xsd>`;

Структуры
---------

Для документов, возникающих в ходе документооборота электронных актов, в Диадоке зарезервированы специальные :doc:`типы сущностей <../proto/Entity message>`.

Для титула исполнителя электронного акта можно использовать следующий структуры:

-  *Attachment/XmlAcceptanceCertificate* (приказ `№ ММВ-7-6/172@ <https://normativ.kontur.ru/document?moduleId=1&documentId=249567>`__),

-  *Attachment/UniversalTransferDocument* (УПД с функцией ДОП, *FunctionType.Basic*, `приказ N ММВ-7-15/155@ <https://normativ.kontur.ru/document?moduleId=1&documentId=271958>`__),

Для титула покупателя электронной накладной можно использовать следующий структуры:

-  *Attachment/XmlAcceptanceCertificateBuyerTitle* (приказ `№ ММВ-7-6/172@ <https://normativ.kontur.ru/document?moduleId=1&documentId=249567>`__),

-  *Attachment/UniversalTransferDocumentBuyerTitle* (исправление УПД с функцией ДОП, *FunctionType.Basic*, `приказ N ММВ-7-15/155@ <https://normativ.kontur.ru/document?moduleId=1&documentId=271958>`__),

Порядок обмена
--------------

.. note::
    Порядок обмена электронными актами между компаниями через Диадок описан `здесь <https://wiki.diadoc.ru/pages/viewpage.action?pageId=1147084>`__

Схема, приведенная ниже, демонстрирует порядок обмена электронными актами, реализованный в Диадоке:

#.  Исполнитель формирует титул исполнителя акта XmlAcceptanceCertificate\ :sub:`1`\, подписывает его и направляет Заказчику.

#.  Диадок доставляет титул исполнителя XmlAcceptanceCertificate\ :sub:`1`\ до Заказчика.

#.  Заказчик получает титул исполнителя акта XmlAcceptanceCertificate\ :sub:`1`\, и формирует в ответ титул заказчика XmlAcceptanceCertificateBuyerTitle\ :sub:`1`\, подписывает его и отправляет в сторону Исполнителя.

#.  Диадок доставляет титул заказчика XmlAcceptanceCertificate\ :sub:`1`\ до Исполнителя.

#.  Если Заказчик обнаружил ошибки в полученном титуле исполнителя акта, он формирует отказ в подписи XmlSignatureRejection\ :sub:`1`\, подписывает его и направляет Исполнителя.

#.  Диадок доставляет отказ в подписи XmlSignatureRejection\ :sub:`1`\ до Исполнителя.
