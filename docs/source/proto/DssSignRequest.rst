DssSignRequest
==============

Структура ``DssSignRequest`` представляет собой запрос на подписание файлов.

.. code-block:: protobuf

    message DssSignRequest {
        repeated DssSignFile Files = 1;
    }

    message DssSignFile {
        required Content_v3 Content = 1;
        optional string FileName = 2;
    }


- ``Files`` — список файлов для подписания, представленных представлен структурой ``DssSignFile`` с полями:

	- ``Content`` — содержимое файла, представеленное структурой :doc:`Content_v3`.
	- ``FileName`` — имя файла.


----

.. rubric:: См. также

*Структура используется:*
	- в теле запроса метода :doc:`../http/DssSign`