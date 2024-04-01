PowerOfAttorneySendingType
==========================

Перечисление ``PowerOfAttorneySendingType`` представляет собой способ передачи машиночитаемой доверенности (МЧД).

.. code-block:: protobuf

	enum PowerOfAttorneySendingType {
		Metadata = 1;
		File = 2;
		DocumentContent - 3;
	}

- ``Metadata`` — МЧД передана в виде мета-информации.
- ``File`` — МЧД отправлена в пакете с документом.
- ``DocumentContent`` — МЧД передана в содержимом документа.

----

.. rubric:: См. также

*Структура используется:*
	- в структуре :doc:`PowerOfAttorneyInfo`,
	- в структуре :doc:`SignaturePowerOfAttorney`.