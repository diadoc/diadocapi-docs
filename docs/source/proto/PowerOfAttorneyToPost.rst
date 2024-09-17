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

- ``FullId`` — идентификатор МЧД, представленный структурой :doc:`PowerOfAttorneyFullId`. Необязательный параметр. Если не указан, то у сотрудника должна быть настроена МЧД по умолчанию и указано значение ``UseDefault = true``.

- ``UseDefault`` — флаг «Использовать МЧД по умолчанию». Чтобы использовать этот флаг, сотрудник или администратор ящика должен настроить МЧД по умолчанию в веб-интерфейсе или с помощью метода :doc:`../http/UpdateEmployeePowerOfAttorney`. Если для сотрудника, вызывающего метод отправки документа, не настроена МЧД по умолчанию, то при значении ``UseDefault = true`` метод вернет ошибку. Если флаг отсутствует, будет установлено значение по умолчанию ``UseDefault = false``.

- ``Content`` — содержимое файла МЧД и подписи. Поле устарело, вместо него используйте поле ``Contents``. Представлено структурой :doc:`PowerOfAttorneySignedContent`.

- ``SendAsFile`` — флаг, указывающий, что МЧД нужно передать файлом. По умолчанию имеет значение ``false``.

  Значение флага учитывается только в случае, если заполнено поле ``FullId`` или ``UseDefault = true``.
  Значение флага не учитывается, если заполнены поля ``Content``, ``Contents`` или ``UseDocumentContent``.

  Не используйте флаг ``SendAsFile``, если МЧД не зарегистрирована в реестре доверенностей ФНС; в этом случае можно передать файл с помощью поля ``Contents``.

- ``Contents`` — список файлов передоверенной МЧД и родительских МЧД. Доверенности могут быть указаны в произвольном порядке. Можно передать содержимое МЧД без передоверия. Каждый файл представлен структурой :doc:`PowerOfAttorneySignedContent`.

- ``UseDocumentContent`` — флаг, указывающий, что МЧД передается в содержимом документа. По умолчанию имеет значение ``false``. Подробнее о передаче МЧД в содержимом в разделе :ref:`powerofattorney_send`. Применимо только для:

  - актов сверки в формате приказа №405,
  - актов о приемке выполненных работ КС-2 в формате приказа №691,
  - УПД в формате приказа ФНС № 970.

В структуре ``PowerOfAttorneyToPost`` можно указать только одно из перечисленных ниже значений, иначе метод отправки вернет ошибку:

	- ``FullId``,
	- ``UseDefault = true``,
	- ``Content``,
	- ``Contents``,
	- ``UseDocumentContent = true``.

Если одновременно указны флаги ``SendAsFile = true`` и ``UseDocumentContent = true``, то МЧД будет передана в содержимом документа.

.. note::

	На время переходного периода допускается отправка документов без МЧД: для этого структура ``PowerOfAttorneyToPost`` должна отсутствовать в теле запроса.


----

.. rubric:: См. также

*Структура используется:*
	- в структуре :doc:`DocumentSenderSignature`
	- в структуре :doc:`DocumentSignature`
	- в структуре :doc:`SignedContent`

*Инструкции:*
	- :doc:`../instructions/powerofattorney`