CloudSignRequest
================

.. code-block:: protobuf

            message CloudSignRequest {
                repeated CloudSignFile Files = 1;
            }

            message CloudSignFile {
                optional Content_v2 Content = 1;
                optional string FileName = 2;
            }
        

*CloudSignRequest* - массив файлов для облачного подписания.

*CloudSignFile* - файл для подписания:

-  *FileName* - имя файла, который пользователь увидит в отчете об использовании свой облачной ЭЦП

-  *Content* - содержимое файла или ссылка на файл. Подробнее в описании :doc:`Content_v2 <Content_v2>`.