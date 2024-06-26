PowerOfAttorneyToRegister
=========================

Структура ``PowerOfAttorneyToRegister`` хранит данные для :doc:`регистрации <../http/RegisterPowerOfAttorney>` машиночитаемой доверенности (МЧД).

.. code-block:: protobuf

    message PowerOfAttorneyToRegister {
        optional PowerOfAttorneyFullId FullId = 1;
        optional PowerOfAttorneySignedContent Content = 2;
    }

- ``FullId`` — идентификатор МЧД, представленный структурой :doc:`PowerOfAttorneyFullId`. Используется в случае регистрации по идентификатору.
- ``Content`` — содержимое файла МЧД с подписью. Используется в случае регистрации с помощью файла с подписью. Представлен структурой :doc:`PowerOfAttorneySignedContent`.

При :doc:`регистрации <../http/RegisterPowerOfAttorney>` МЧД в структуре обязательно нужно указать либо параметр ``FullId``, либо параметр ``Content``. Указание обоих параметров одновременно недопустимо.


----

.. rubric:: См. также

*Структура используется:*
	- в теле запроса метода :doc:`../http/RegisterPowerOfAttorney`

*Инструкции:*
	- :doc:`../instructions/powerofattorney`