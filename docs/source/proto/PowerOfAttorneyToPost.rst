PowerOfAttorneyToPost
=====================

Структура ``PowerOfAttorneyToPost`` предназначена для заполнения данных о машиночитаемой доверенности (МЧД) при отправке документов.

.. code-block:: protobuf

    message PowerOfAttorneyToPost {
        optional PowerOfAttorneyFullId FullId = 1;
        required bool UseDefault = 2;
        optional PowerOfAttorneySignedContent Content = 3;
        optional bool SendAsFile = 4;
        repeated PowerOfAttorneySignedContent Contents = 5;
    }

    message PowerOfAttorneySignedContent {
        required Content_v3 Content = 1;
        required Content_v3 Signature = 2;
    }

- ``FullId`` — идентификатор МЧД. Представлен структурой :doc:`PowerOfAttorneyFullId`. Необязательный параметр. Если не указан, то у сотрудника должна быть настроена МЧД по умолчанию и флаг ``UseDefault`` должен иметь значение ``true``.
- ``UseDefault`` — флаг «Использовать МЧД по умолчанию». Чтобы использовать этот флаг, сотрудник или администратор ящика должен настроить МЧД по умолчанию в веб-интерфейсе или с помощью метода :doc:`../http/UpdateEmployeePowerOfAttorney`. Если для сотрудника, вызывающего метод отправки документа, не настроена МЧД по умолчанию, то при значении ``UseDefault=true`` метод вернет ошибку.
- ``Content`` — содержимое файла МЧД и подписи. Поле устарело. Рекомендуем использовать ``Contents``. Содержимое представлено структурой ``PowerOfAttorneySignedContent`` с полями:

	- ``Content`` — файл МЧД. Представлен структурой :doc:`Content_v3`.
	- ``Signature`` — файл подписи под МЧД. Представлен структурой :doc:`Content_v3`.

- ``SendAsFile`` — флаг, указывающий, что МЧД нужно передать файлом. По умолчанию имеет значение ``false``. МЧД будет передана файлом, если заполнено поле ``FullId`` или ``UseDefault=true`` и ``SendAsFile=true``. Не используйте флаг ``SendAsFile``, если МЧД не зарегистрирована в реестре доверенностей ФНС. В этом случае передать файл можно с помощью структуры :doc:`Content`.

- ``Contents`` — список файлов передоверенной МЧД и родительских МЧД. Доверенности могут быть указаны в произвольном порядке. Можно передать содержимое МЧД без передоверия. Каждый файл представлен структурой ``PowerOfAttorneySignedContent`` с полями:

	- ``Content`` — файл МЧД. Представлен структурой :doc:`Content_v3`.
	- ``Signature`` — файл подписи под МЧД. Представлен структурой :doc:`Content_v3`.

В структуре ``PowerOfAttorneyToPost`` должно быть указано либо значение ``UseDefault=true``, либо одно из полей: ``FullId``, ``Content``, ``Contents``. Иначе метод отправки вернет ошибку.
Нельзя одновременно указывать значения в полях ``FullId``, ``Content`` и ``Contents`` и параметр ``UseDefault=true``.

.. note::

	На время переходного периода допускается отправка документов без МЧД: для этого структура ``PowerOfAttorneyToPost`` должна отсутствовать в теле запроса.

----

.. rubric:: Смотри также

*Структура используется:*
	- в структуре :doc:`SignedContent`,
	- в структуре :doc:`DocumentSignature`,
	- в структуре :doc:`DocumentSenderSignature`.
	
*Руководства:*
	- :doc:`Как работать с МЧД <../howto/powerofattorney>`