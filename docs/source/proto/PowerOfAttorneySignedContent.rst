PowerOfAttorneySignedContent
============================

Структура ``PowerOfAttorneySignedContent`` представляет собой содержимое файла машиночитаемой доверенности (МЧД) с подписью.

.. code-block:: protobuf

    message PowerOfAttorneySignedContent {
        required Content_v3 Content = 1;
        required Content_v3 Signature = 2;
    }

- ``Content`` — файл МЧД, представленный структурой :doc:`Content_v3`.
- ``Signature`` — файл подписи под МЧД, представленный структурой :doc:`Content_v3`.


----

.. rubric:: См. также

*Структура используется:*
	- в структуре :doc:`PowerOfAttorneyToPost`
	- в структуре :doc:`PowerOfAttorneyToRegister`

*Инструкции:*
	- :doc:`../instructions/powerofattorney`