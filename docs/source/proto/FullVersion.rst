FullVersion
===========

.. code-block:: protobuf

    message FullVersion {
        required string TypeNamedId = 1;
        required string Function = 2;
        required string Version = 3;
    }

Структура описывает тип, функцию и версию документа.

-  *TypeNamedId* - строковой идентификатор типа документа
-  *Function* - строковой идентификатор функции документа
-  *Version* - строковой идентификатор версии документа

Описания типов, функций и версий можно получить методом :doc:`../http/GetDocumentTypes`.
