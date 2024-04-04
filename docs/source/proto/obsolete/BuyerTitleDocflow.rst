BuyerTitleDocflow
=================

.. warning::
	Структура относится к устаревшей версии Docflow API. Используйте последнюю версию :doc:`../../Docflow API` — V3.

Структура ``BuyerTitleDocflow`` представляет собой информацию об ответной подписи под двусторонним формализованным документом (титул покупателя). Ответная подпись в этом случае является подписанным формализованным файлом установленного формата.

.. code-block:: protobuf

   message BuyerTitleDocflow
   {
       optional bool IsFinished = 1;
       optional SignedAttachment BuyerTitleAttachment = 2;
       optional Timestamp SendTimestamp = 3;
       optional Timestamp DeliveryTimestamp = 4;
   }

- ``IsFinished`` — признак того, что документооборот завершен и документ не требует дальнейших действий. Принимает значение ``true`` в случае если подпись под титулом покупателя проверена и он доставлен контрагенту.
- ``BuyerTitleAttachment`` — информация о файле титула покупателя, представленное структурой :doc:`../SignedAttachment`.
- ``SendTimestamp`` — время отправки титула покупателя, представленное структурой :doc:`../Timestamp`.
- ``DeliveryTimestamp`` — время доставки титула покупателя, представленное структурой :doc:`../Timestamp`.

----

.. rubric:: См. также

*Структура используется:*
	- в структуре :doc:`InboundUniversalTransferDocumentDocflow`,
	- в структуре :doc:`OutboundUniversalTransferDocumentDocflow`,
	- в структуре :doc:`XmlBilateralDocflow`.

*Руководства:*
	- :doc:`../../Docflow API`