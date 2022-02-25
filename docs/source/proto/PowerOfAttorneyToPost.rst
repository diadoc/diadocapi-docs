PowerOfAttorneyToPost
=====================

Структура ``PowerOfAttorneyToPost`` предназначена для заполнения данных о машиночитаемой доверенности (МЧД) при отправке документов.

.. code-block:: protobuf

    message PowerOfAttorneyToPost {
        optional PowerOfAttorneyFullId FullId = 1;
        required bool UseDefault = 2;
    }
   
- ``FullId`` — идентификатор МЧД, представленный структурой :doc:`PowerOfAttorneyFullId`, необязательный параметр. Если не указан, то у сотрудника должна быть настроена МЧД по умолчанию и флаг ``UseDefault`` должен иметь значение ``true``.
- ``UseDefault`` — флаг «Использовать МЧД по умолчанию». Для его применения нужно настроить МЧД по умолчанию в веб-интерфейсе или через API. Если для сотрудника, вызывающего метод отправки документа, не настроена МЧД по умолчанию, то при значении ``UseDefault=true`` метод вернет ошибку.

В структуре ``PowerOfAttorneyToPost`` обязательно должно быть указано либо поле ``FullId``, либо значение ``UseDefault=true``. В противном случае метод отправки вернет ошибку.
Нельзя одновременно указывать значение ``FullId`` и параметр  ``UseDefault=true``.

.. note::

	На время переходного периода допускается отправка документов без МЧД: для этого структура ``PowerOfAttorneyToPost`` должна отсутствовать в теле запроса.

----

.. rubric:: Использование

Структура ``PowerOfAttorneyToPost`` используется внутри структур:

- :doc:`SignedContent`
- :doc:`DocumentSignature`
- :doc:`DocumentSenderSignature`
