SignerType
==========

Перечисление ``SignerType`` представляет собой тип подписанта.

.. code-block:: protobuf

    enum SignerType {
        Unspecified = -1;
        LegalEntity = 1;
        IndividualEntity = 2;
        PhysicalPerson = 3;
    }

- ``Unspecified`` — неизвестный тип подписанта.
- ``LegalEntity`` — представитель юридического лица.
- ``IndividualEntity`` — индивидуальный предприниматель.
- ``PhysicalPerson`` — физическое лицо.

----

.. rubric:: Смотри также

*Перечисление используется:*
	- в структуре :doc:`ExtendedSignerToPost`,
	- в структуре :doc:`utd/ExtendedSigner`, возвращаемой методом  :doc:`../http/utd/ExtendedSignerDetailsV2`.