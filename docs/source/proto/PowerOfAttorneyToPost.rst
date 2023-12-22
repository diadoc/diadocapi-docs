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
        optional bool UseDocumentContent = 6;
    }

    message PowerOfAttorneySignedContent {
        required Content_v3 Content = 1;
        required Content_v3 Signature = 2;
    }

- ``FullId`` — идентификатор МЧД, представленный структурой :doc:`PowerOfAttorneyFullId`. Необязательный параметр. Если не указан, то у сотрудника должна быть настроена МЧД по умолчанию и флаг ``UseDefault`` должен иметь значение ``true``.

- ``UseDefault`` — флаг «Использовать МЧД по умолчанию». Чтобы использовать этот флаг, сотрудник или администратор ящика должен настроить МЧД по умолчанию в веб-интерфейсе или с помощью метода :doc:`../http/UpdateEmployeePowerOfAttorney`. Если для сотрудника, вызывающего метод отправки документа, не настроена МЧД по умолчанию, то при значении ``UseDefault=true`` метод вернет ошибку.

- ``Content`` — содержимое файла МЧД и подписи. Поле устарело; используйте поле ``Contents``. Представлено структурой ``PowerOfAttorneySignedContent`` с полями:

	- ``Content`` — файл МЧД, представленный структурой :doc:`Content_v3`.
	- ``Signature`` — файл подписи под МЧД, представленный структурой :doc:`Content_v3`.

- ``SendAsFile`` — флаг, указывающий, что МЧД нужно передать файлом. По умолчанию имеет значение ``false``. МЧД будет передана файлом, если заполнено поле ``FullId`` или ``UseDefault=true`` и ``SendAsFile=true``. Не используйте флаг ``SendAsFile``, если МЧД не зарегистрирована в реестре доверенностей ФНС; в этом случае можно передать файл с помощью структуры :doc:`Content`.

- ``Contents`` — список файлов передоверенной МЧД и родительских МЧД. Доверенности могут быть указаны в произвольном порядке. Можно передать содержимое МЧД без передоверия. Каждый файл представлен структурой ``PowerOfAttorneySignedContent`` с полями:

	- ``Content`` — файл МЧД. Представлен структурой :doc:`Content_v3`.
	- ``Signature`` — файл подписи под МЧД. Представлен структурой :doc:`Content_v3`.

- ``UseDocumentContent`` — флаг, указывающий, что МЧД передается в содержимом документа. По умолчанию имеет значение ``false``. Применимо только для актов сверки в формате приказа №405. Документ с МЧД в содержимом должен соответствовать :ref:`условиям <powerofattorney_send>`.

В структуре ``PowerOfAttorneyToPost`` может быть заполнено только одно из полей:

	- ``FullId``,
	- ``Content``,
	- ``Contents``,
	- ``UseDefault = true``,
	- ``UseDocumentContent=true``.

Если одновременно указны флаги ``SendAsFile=true`` и ``UseDocumentContent=true``, то МЧД будет передана в содержимом документа.

.. note::

	На время переходного периода допускается отправка документов без МЧД: для этого структура ``PowerOfAttorneyToPost`` должна отсутствовать в теле запроса.

----

.. rubric:: Смотри также

*Структура используется:*
	- в структуре :doc:`SignedContent`,
	- в структуре :doc:`DocumentSignature`,
	- в структуре :doc:`DocumentSenderSignature`.
	
*Руководства:*
	- :doc:`../howto/powerofattorney`.