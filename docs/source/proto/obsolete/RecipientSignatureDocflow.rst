RecipientSignatureDocflow
=========================

.. warning::
	Структура устарела.

Структура ``RecipientSignatureDocflow`` представляет собой информацию об ответной подписи, поставленной контрагентом под документом.

.. code-block:: protobuf

   message RecipientSignatureDocflow
   {
       optional bool IsFinished = 1;
       optional Signature RecipientSignature = 2;
       optional Timestamp DeliveryTimestamp = 3;
   }

- ``IsFinished`` — признак того, что подпись проверена и доставлена контрагенту.
- ``RecipientSignature`` — информация о содержимом подписи, результатах его проверки, и пр. Представлена структурой :doc:`../Signature`.
- ``DeliveryTimestamp`` — время доставки подписи контрагенту, представленное структурой :doc:`../Timestamp`.


----

.. rubric:: См. также

*Структура используется:*
	- в устаревшей структуре :doc:`BilateralDocflow`
	- в устаревшей структуре :doc:`RevocationDocflow`