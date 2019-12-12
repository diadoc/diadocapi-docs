TotalCountType
========

.. code-block:: protobuf

  enum TotalCountType
  {
      Equal = 1;
      GreaterThanOrEqual = 2;
  }

*TotalCountType* — указывает на то, является ли значение `TotalCount` точным или подсчет был ограничен.

	- *Equal* — точное значение

	- *GreaterThanOrEqual* — подсчет ограничен, реальное значение больше или равно указанному.
