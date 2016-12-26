BasicDocumentInfo
=================

.. code-block:: protobuf

    message BasicDocumentInfo
    {
        optional string Total = 1;
        optional bool NoVat = 2;
        optional string Vat = 3;
        optional string Grounds = 4;
    }

Структура представляет метаданные документов, имеющих :doc:`тип <DocumentType>` *XmlTorg12*, *XmlAcceptanceCertificate*, *Torg12*, *AcceptanceCertificate*, *ProformaInvoice* или *Torg13*.

-  *Total* - сумма с учетом НДС, всего по документу.

-  *NoVat* - признак того, что ставка налога по документу равна "без НДС".

-  *Vat* - сумма НДС, всего по документу.

-  *Grounds* - описание оснований для данного документа.
