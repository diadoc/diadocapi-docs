PowerOfAttorneyToRegister
=========================

Структура ``PowerOfAttorneyToRegister`` хранит данные для :doc:`регистрации <../http/RegisterPowerOfAttorney>` машиночитаемой доверенности (МЧД).

.. code-block:: protobuf

    message PowerOfAttorneyToRegister {
        optional PowerOfAttorneyFullId FullId = 1;
        optional PowerOfAttorneySignedContent Content = 2;
    }

    message PowerOfAttorneySignedContent {
        required Content_v3 Content = 1;
        required Content_v3 Signature = 2;
    }
   
- ``FullId`` — идентификатор МЧД, представленный структурой :doc:`PowerOfAttorneyFullId`. Используется в случае регистрации по идентификатору.
- ``Content`` — содержимое файла МЧД с подписью. Используется в случае регистрации с помощью файла с подписью. Представлен структурой ``PowerOfAttorneySignedContent`` с полями:

	- ``Content`` — файл МЧД, представленный структурой :doc:`Content_v3`.
	- ``Signature`` — файл подписи под МЧД, представленный структурой :doc:`Content_v3`.

При :doc:`регистрации <../http/RegisterPowerOfAttorney>` МЧД в структуре обязательно нужно указать либо параметр ``FullId``, либо параметр ``Content``. Указание обоих параметров одновременно недопустимо.

----

.. rubric:: Использование

Структура ``PowerOfAttorneyToRegister`` используется в теле запроса метода :doc:`../http/RegisterPowerOfAttorney`.