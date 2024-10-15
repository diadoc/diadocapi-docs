DocumentTitleType
=================

Перечисление ``DocumentTitleType`` представляет собой тип титула документа.

.. code-block:: protobuf

    enum DocumentTitleType {
        Absent = -1;
        UtdSeller = 0;
        UtdBuyer = 1;
        UcdSeller = 2;
        UcdBuyer = 3;
        TovTorg551Seller = 4;
        TovTorg551Buyer = 5;
        AccCert552Seller = 6;
        AccCert552Buyer = 7;
        Utd820Buyer = 8;
        Torg2Buyer = 9;
        Torg2AdditionalInfo = 10;
        Utd970Seller = 12;
        Utd970Buyer = 13;
    }


- ``Absent`` — зарезервированное значение.
- ``UtdSeller`` — титул продавца УПД.
- ``UtdBuyer`` — титул покупателя УПД.
- ``UcdSeller`` — титул продавца УКД.
- ``UcdBuyer`` — титул покупателя УКД.
- ``TovTorg551Seller`` — титул продавца формата приказа 551.
- ``TovTorg551Buyer`` — титул покупателя формата приказа 551.
- ``AccCert552Seller`` — титул исполнителя формата приказа 552.
- ``AccCert552Buyer`` — титул заказчика формата приказа 552.
- ``Utd820Buyer`` — титул покупателя УПД формата приказа 820.
- ``Torg2Buyer`` — титул покупателя Торг-2.
- ``Torg2AdditionalInfo`` — титул продавца Торг-2.
- ``Utd970Seller`` — титул продавца УПД формата приказа 970.
- ``Utd970Buyer`` — титул покупателя УПД формата приказа 970.


----

.. rubric:: См. также

*Перечисление используется:*
	- в параметре запроса метода :doc:`../http/ExtendedSignerDetailsV2`
	- в устаревшей структуре :ref:`SignerInfo`