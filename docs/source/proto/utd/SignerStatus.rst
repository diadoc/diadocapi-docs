SignerStatus
============

Перечисление ``SignerStatus`` представляет собой статус подписанта.

.. code-block:: protobuf

    enum SignerStatus {
        Unspecified = -1;
        SellerEmployee = 1;
        InformationCreatorEmployee = 2;
        OtherOrganizationEmployee = 3;
        AuthorizedPerson= 4;
        BuyerEmployee = 5;
        InformationCreatorBuyerEmployee = 6;
    }

- ``Unspecified`` — неизвестный статус подписанта.
- ``SellerEmployee`` — работник организации-продавца товаров, работ, услуг, имущественных прав.
- ``InformationCreatorEmployee`` — работник организации-составителя информации продавца.
- ``OtherOrganizationEmployee`` — работник иной уполномоченной организации.
- ``AuthorizedPerson`` — уполномоченное физическое лицо, в том числе индивидуальный предприниматель
- ``BuyerEmployee`` — работник организации-покупателя. Используется для документов в формате приказа №820.
- ``InformationCreatorBuyerEmployee`` — работник организации-составителя файла обмена информации покупателя, если составитель файла обмена информации покупателя не является покупателем. Используется для документов в формате приказов №820 и №423.

----

.. rubric:: Смотри также

*Перечисление используется:*
	- в структуре :doc:`ExtendedSignerDetailsToPost`
	- в структуре :doc:`ExtendedSigner`, возвращаемой методом

		- :doc:`../../http/utd/ExtendedSignerDetailsV2`.