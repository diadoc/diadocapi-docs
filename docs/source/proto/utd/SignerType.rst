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

*Структура[/Перечисление] используется:*
	- в структуре :doc:`ExtendedSignerDetailsToPost`
	- в структуре :doc:`ExtendedSigner`, возвращаемой методом

		- :doc:`../../http/ExtendedSignerDetails`.
	