SignerPowers
============

Перечисление ``SignerPowers`` представляет собой область полномочий подписанта.

.. code-block:: protobuf

    
    enum SignerPowers {
        SignerPowersUnspecified = -1;
        InvoiceSigner = 0;
        PersonMadeOperation = 1;
        MadeAndSignOperation = 2;
        PersonDocumentedOperation = 3;
        MadeOperationAndSignedInvoice = 4;
        MadeAndResponsibleForOperationAndSignedInvoice = 5;
        ResponsibleForOperationAndSignerForInvoice = 6;
        ChairmanCommission = 7;
        MemberCommission = 8;
        PersonApprovedDocument = 21;
        PersonConfirmedDocument = 22;
        PersonAgreedOnDocument = 23;
        PersonOtherPower = 29;
    }

- ``SignerPowersUnspecified`` — неизвестная область полномочий подписанта.
- ``InvoiceSigner`` — лицо, ответственное за подписание счетов-фактур.
- ``PersonMadeOperation`` — лицо, совершившее сделку, операцию.
- ``MadeAndSignOperation`` — лицо, совершившее сделку, операцию и ответственное за её оформление.
- ``PersonDocumentedOperation`` — лицо, ответственное за оформление свершившегося события.
- ``MadeOperationAndSignedInvoice`` — лицо, совершившее сделку, операцию и ответственное за подписание счетов-фактур.
- ``MadeAndResponsibleForOperationAndSignedInvoice`` — лицо, совершившее сделку, операцию и ответственное за её оформление и за подписание счетов-фактур.
- ``ResponsibleForOperationAndSignerForInvoice`` — лицо, ответственное за оформление свершившегося события и за подписание счетов-фактур.
- ``ChairmanCommission`` — председатель комиссии.
- ``MemberCommission`` — член комиссии.
- ``PersonApprovedDocument`` — лицо, в полномочия которого входит утверждение документа, оформляющего событие (факт хозяйственной жизни).
- ``PersonConfirmedDocument`` — лицо, в полномочия которого входит подтверждение оформленного события (факта хозяйственной жизни).
- ``PersonAgreedOnDocument``— лицо, в полномочия которого входит согласование документа, оформляющего событие (факт хозяйственной жизни).
- ``PersonOtherPower`` — лицо с иными полномочиями.

----

.. rubric:: См. также

*Перечисление используется:*
	- в структуре :doc:`ExtendedSigner`
	- в структуре :doc:`ExtendedSignerDetailsToPost`
