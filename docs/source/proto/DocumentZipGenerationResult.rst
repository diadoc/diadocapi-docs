DocumentZipGenerationResult
===========================

.. code-block:: protobuf

    message DocumentZipGenerationResult {
        optional string ZipFileNameOnShelf = 1;
    }
        

Структура данных *DocumentZipGenerationResult* представляет результат формирования zip-архива методом :doc:`../http/GenerateDocumentZip`:

-  *ZipFileNameOnShelf* - полный путь к файлу архива на «полке документов». 

Если архив уже сформирован, его можно скачать методом :doc:`../http/ShelfDownload`. Если архив еще не готов, данное поле возвращается пустым.