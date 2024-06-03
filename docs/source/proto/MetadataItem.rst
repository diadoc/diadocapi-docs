MetadataItem
============

Представляет пару "ключ-значение", привязанную к документу в качестве метаданных.

.. code-block:: protobuf

    message MetadataItem {
        required string Key = 1;
        required string Value = 2;
    }

-  *Key* - непустой ключ. Должен быть валидным ключом метаданных для данного типа документа. Список доступных метаданных для типа можно получить через метод :doc:`../http/GetDocumentTypes`. Инструкция о получении данных из метода ``GetDocumentTypes`` приведена на странице :doc:`../instructions/getdoctypes`.
-  *Value* - непустое значение, соответствующее ключу Key.
