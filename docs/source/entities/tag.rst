Тег (CustomData, пользовательские данные)
=========================================

**Тег документа** — пользовательские данные, привязанные к документу в виде произвольной пары «ключ-значение». В API Диадока имеют название ``CustomData``.

Теги можно использовать для записи технических параметров документа, для организации поиска документа, для маршрутизации документа и других целей.

Структура
---------

Тег представляет собой структуру, состоящую из ключа ``Key`` и значения ``Value``:

- ``Key`` — название тега, произвольный ключ. Не может быть пустым. Регистронезависимый. Может содержать только буквы латинского и русского алфавита, цифры и символы «-» и «_». Длина не может превышать 60 символов.

 Название тега должно быть уникальным в рамках одного документа, то есть у документа не может быть несколько тегов с названием «Номер_договора» и разными значениями. 

 Пример ключа: «Номер_договора», «Subdivision».
 
- ``Value`` — значение тега, соответствующее ключу ``Key``. Может быть пустым. Регистронезависимый. Длина не может превышать 200 символа.

 Пример значения: «DOC2356», «Бухгалтерия».

Использование
-------------

- Присвоить теги документу можно при отправке методом :doc:`../http/PostMessage`, передав в него структуру :doc:`../proto/MessageToPost` с заполненным полем :doc:`DocumentAttachment.CustomDataItem <../proto/DocumentAttachment>`.
- Присвоить теги шаблону можно при отправке методом :doc:`../http/PostTemplate`, передав в него структуру :doc:`../proto/TemplateToPost` с заполненным полем :doc:`TemplateDocumentAttachment.CustomDataItem <../proto/TemplateDocumentAttachment>`.
- Отредактировать теги, удалить или добавить новые можно с помощью метода :doc:`../http/PostMessagePatch`, передав в него структуру :doc:`../proto/MessagePatchToPost` с заполненным полем :doc:`../proto/CustomDataPatch`.
- Искать документы по тегам можно с помощью метода :doc:`../http/SearchDocflows_V3`.

Для работы с тегами в API не нужно дополнительных настроек. Функциональность доступна всем пользователям.

Особенности
-----------

- Все изменения с тегами документа сквозные: если отправитель присвоил документу теги, то получатель сможет их увидеть (через API или в Web-версии Диадока, если у него включена такая возможность).
- Изменять теги и видеть произошедшие изменения могут все стороны документооборота: отправитель, промежуточный и конечный получатель.
- В роуминге можно работать только со ограниченным списком разрешенных тегов. Чтобы добавить тег в список разрешенных, обратитесь к менеджеру или в `техническую поддержку <https://www.diadoc.ru/support>`__.
- При трансформации шаблона в документ его теги будут скопированы.
- В Web-версии Диадока теги шаблонов не отображаются, даже если у пользователя включена возможность просматривать теги документов.

Ограничения
-----------

- У документа может быть не более 30 неудаленных тегов.
- У документа можно отредактировать теги не более 10 раз: добавить новые, изменить или удалить существующие.
- Нельзя добавить, изменить или удалить теги для отправленного шаблона.


----

.. rubric:: Представление в API

В API теги представлены структурами:

	- :doc:`../proto/CustomDataItem` — при отправке сообщения
	- :doc:`../proto/CustomDataPatch` — при изменении сообщения