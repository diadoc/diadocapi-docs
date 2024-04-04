BasicDocumentInfo
=================

.. warning::
	Структура относится к устаревшей версии Docflow API. Используйте последнюю версию :doc:`../../Docflow API` — V3.

Структура ``BasicDocumentInfo`` представляет собой метаданные документов, имеющих :doc:`тип <DocumentType>`:

   - ``XmlTorg12``,
   - ``XmlAcceptanceCertificate``,
   - ``Torg12``,
   - ``AcceptanceCertificate``,
   - ``ProformaInvoice``, 
   - ``Torg13``.

.. code-block:: protobuf

    message BasicDocumentInfo
    {
        optional string Total = 1;
        optional bool NoVat = 2;
        optional string Vat = 3;
        optional string Grounds = 4;
    }

- ``Total`` — сумма с учетом НДС, всего по документу.
- ``NoVat`` — признак, что ставка налога по документу равна «без НДС».
- ``Vat`` — сумма НДС, всего по документу.
- ``Grounds`` — описание оснований для данного документа.

----

.. rubric:: См. также

*Структура используется:*
	- в структуре :doc:`DocumentInfo`