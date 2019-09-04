DssSignRequest
==============

.. code-block:: protobuf

    message DssSignRequest {
        repeated DssSignFile Files = 1;
    }
        

-  :ref:`Files <dss-sign-file>` - список файлов для подписания

Структура описывает запрос на подписание файлов DSS-сертификатом. Принимается методом :doc:`../http/DssSign`.

.. _dss-sign-file:

DssSignFile
-----------

Описывает файл для подписания.

.. code-block:: protobuf

        message DssSignFile {
            required Content_v3 Content = 1;
            optional string FileName = 2;
        }

-  :doc:`Content_v3` - содержимое файла
-  *FileName* - имя файла