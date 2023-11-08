PowerOfAttorneySendingType
==========================

Перечисление ``PowerOfAttorneySendingType`` представляет собой способ передачи машиночитаемой доверенности (МЧД).

.. code-block:: protobuf

	enum PowerOfAttorneySendingType {
		Metadata = 1;
		File = 2;
		XmlContent - 3;
	}

- ``Metadata`` — МЧД передали в виде мета-информации.
- ``File`` — МЧД отправили в пакете с документом.
- ``XmlContent`` — МЧД передали в содержимом документа.

----

.. rubric:: Смотри также

*Структура используется:*
	- в структуре :doc:`PowerOfAttorneyInfo`,
	- в структуре :doc:`SignaturePowerOfAttorney`.