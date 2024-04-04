SignerType
==========

Перечисление ``SignerType`` представляет собой тип подписанта.

.. code-block:: protobuf

    enum SignerType {
        SignerTypeUnspecified = -1;
        LegalEntity = 1;
        IndividualEntity = 2;
        PhysicalPerson = 3;
    }

- ``SignerTypeUnspecified`` — неизвестный тип подписанта.
- ``LegalEntity`` — представитель юридического лица.
- ``IndividualEntity`` — индивидуальный предприниматель.
- ``PhysicalPerson`` — физическое лицо.

----

.. rubric:: См. также

*Перечисление используется:*
	- в структуре :doc:`ExtendedSignerDetailsToPost`
	- в структуре :doc:`utd/ExtendedSigner`