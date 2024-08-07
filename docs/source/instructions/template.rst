Работа с шаблонами
==================

.. contents:: :local:
	:depth: 3

Определение шаблона приведено на странице :doc:`../entities/template`.

Сценарии использования шаблонов
-------------------------------

- У получателя документа есть определенные требования к этому документу. Получатель может сам создать шаблон документа, удовлетворяющего этим требованиям, и передать этот шаблон отправителю документа. Отправитель создаст документ на основе шаблона и отправит его получателю. Так получателю придет документ, который удовлетворяет его требованиям.
- У получателя документов много контрагентов. Получатель хочет уменьшить количество ошибок во входящих документах. Он может создать шаблон и отправить его контрагентам. Так получатель будет уверен, что получит от контрагентов документы без ошибок.
- Отправитель документа хочет показать документ получателю до его подписания. Он может создать шаблон и отправить его получателю для ознакомления. Когда получатель подтвердит, что документ соответствует его ожиданиям, отправитель создаст документ из шаблона и отправит его получателю.
- Отправитель документа не знает, как должен выглядеть отправляемый документ. Он просит третью сторону подготовить для него шаблон документа, который нужно отправить получателю. Третья сторона готовит шаблон и передает его отправителю. Отправитель создает из шаблона документ и отправляет получателю.


Возможности и ограничения шаблонов
----------------------------------

- Из шаблона можно создать юридически значимый документ :doc:`любого типа <../http/GetDocumentTypes>`.
- Шаблоны можно связать в пакет, в том числе в закрытый. Шаблоны из закрытого пакета могут быть обработаны только вместе. Документы, созданные из шаблонов в закрытом пакете, будут отправлены в пакете, состав которого изменить нельзя.
- Шаблоны могут быть одноразовыми и многоразовыми. На основе одноразового шаблона можно создать только один документ, на основе многоразового — неограниченное количество документов.
- В шаблоне можно указать настройки будущего документа: запрос подписи, данные о документе и т.д.
- Шаблоны могут быть редактируемыми, то есть их настройки можно будет изменить перед отправкой.
- Функционал шаблонов недоступен по умолчанию. Чтобы получить возможность отправлять шаблоны, обратитесь к вашему менеджеру или в `техническую поддержку <https://www.diadoc.ru/support>`__.


Действия с шаблонами
--------------------

Организации могут производить с шаблонами следующие действия.

- Отправитель шаблона может:
	- :ref:`настроить и отправить шаблон получателю <template_send>`,
	- :ref:`отозвать отправленный шаблон <template_refuse>`.
 
- Получатель шаблона может:
	- :ref:`отклонить шаблон <template_refuse>`.
 
- Обе стороны могут:
	- :ref:`создать из шаблона документ <template_create_doc>`,
	- :ref:`получить шаблон по идентификаторам или получить список событий по шаблону <template_get>`,
	- :ref:`удалить, восстановить или переместить шаблон <template_other_action>`.


.. _template_send:

Отправка шаблона
~~~~~~~~~~~~~~~~

Чтобы отправить шаблон, вызовите метод :doc:`../http/PostTemplate` и передайте в него заполненную структуру :doc:`../proto/TemplateToPost` — она должна содержать сведения об отправляемом шаблоне.

Особенности заполнения структуры ``TemplateToPost``:

- Структура ``TemplateToPost`` должна содержать список документов :doc:`../proto/TemplateDocumentAttachment`, которые отправляются в шаблоне.
- Получатель шаблона может :ref:`отклонить документ из шаблона <template_refuse>`. Чтобы запретить отклонение, установите значение свойства ``TemplateDocumentAttachment.RefusalDisabled = true``.
- Чтобы сделать многоразовый шаблон, установите значение свойства ``TemplateToPost.IsReusable = true``.
- По умолчанию нельзя редактировать документы, созданные из шаблона, перед их отправкой. Чтобы сделать шаблон редактируемым, задайте для шаблона :ref:`настройки редактирования <template_editing>`.
- Организацию, которая сможет создать документ из шаблона, нужно указать при отправке шаблона в поле ``TemplateToPost.MessageFromBoxId``.

Ниже перечислены примеры заполнения значений ящиков в структуре ``TemplateToPost`` в зависимости от схемы использования шаблона.


Схемы использования шаблонов
""""""""""""""""""""""""""""

**1. Документ готовит получатель**

 В этой схеме получатель документа подготавливает его за отправителя.

 1. Организация *boxId1* создает шаблон и отправляет его организации *boxId2*.
 2. Организация *boxId2* получает шаблон, создает из него документ и отправляет его организации *boxId1*.
 3. Организация *boxId1*, которая отправила шаблон, получает от организации *boxId2* входящий документ, созданный из этого шаблона.

 .. image:: ../_static/img/template_dockflow_schema1.png
	:align: center

 Чтобы отправить документ по этой схеме, идентификаторы ящиков в структуре :doc:`../proto/TemplateToPost` нужно заполнить так:
 ::

	"FromBoxId": "boxId1",
	"ToBoxId": "boxId2",
	"MessageFromBoxId": "boxId2",
	"MessageToBoxId": "boxId1"

	
**2. Предварительный просмотр документа**

 В этой схеме шаблон используется для предварительного просмотра документа будущим получателем.

 1. Организация *boxId1* создает шаблон и отправляет его организации *boxId2*.
 2. Организация *boxId2* получает шаблон и знакомится с его содержимым.
 3. Организация *boxId1*, которая создала шаблон, теперь создает документ из этого шаблона и отправляет его организации *boxId2*.
 4. Организация *boxId2* получает документ, созданный из шаблона, с которым ознакомилась ранее.

 .. image:: ../_static/img/template_dockflow_schema2.png
	:align: center

 Чтобы отправить документ по этой схеме, идентификаторы ящиков в структуре :doc:`../proto/TemplateToPost` нужно заполнить так:
 ::

	"FromBoxId": "boxId1",
	"ToBoxId": "boxId2",
	"MessageFromBoxId": "boxId1",
	"MessageToBoxId": "boxId2"

	
**3. Документ готовит третья сторона**

 В этой схеме документ подготавливает сторона, не участвующая в юридически значимом документообороте. Получатель документа не имеет доступа к шаблону. Шаблон согласовывают между собой две организации, документ получает третья организация.

 1. Организация *boxId1* создает шаблон и отправляет ее организации *boxId2*.
 2. Организация *boxId2* получает шаблон, создает из него документ и отправляет его организации *boxId3*.
 3. Организация *boxId3* получает документ, но не имеет доступа к шаблону, из которого он был создан.

 .. image:: ../_static/img/template_dockflow_schema3.png
	:align: center

 Чтобы отправить документ по этой схеме, идентификаторы ящиков в структуре :doc:`../proto/TemplateToPost` нужно заполнить так:
 ::

	"FromBoxId": "boxId1",
	"ToBoxId": "boxId2",
	"MessageFromBoxId": "boxId2",
	"MessageToBoxId": "boxId3"


.. _template_editing:

Редактируемые шаблоны
"""""""""""""""""""""

Чтобы сделать шаблон редактируемым, к нему нужно применить :doc:`настройки редактирования <editingsettings>`. Для этого выполните следующие действия:

- Заполните структуру :doc:`../proto/TemplateToPost`
- В поле ``TemplateToPost.TemplateDocumentAttachment.UnsignedContent.Content`` поместите бинарное содержимое документа. Если нужно, оставьте в нем пустыми те поля, которые требуется отредактировать перед отправкой.
- В поле ``TemplateToPost.TemplateDocumentAttachment.EditingSettingId`` укажите значение идентификатора настройки редактирования, полученного у вашего менеджера.


.. _template_get:

Получение шаблонов и событий
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Получить шаблон по идентификаторам можно с помощью метода :doc:`../http/GetMessage`.

Получить события по шаблонам можно с помощью методов:

- :doc:`../http/GetNewEvents`
- :doc:`../http/GetDocflows_V3`
- :doc:`../http/GetMessage`


.. _template_create_doc:

Создание документа из шаблона
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Чтобы создать документ из шаблона, вызовите метод :doc:`../http/TransformTemplateToMessage`.

.. important::
	Создать документ может только организация, ящик которой указан в поле ``MessageFromBoxId`` структуры :doc:`../proto/TemplateToPost` при отправке шаблона.

Особенности создания документа из шаблона:

- Если шаблон был создан с :doc:`настройками редактирования <editingsettings>`, то созданный из него документ необходимо дозаполнить перед отправкой. Чтобы заполнить документ, отправьте :doc:`патч <../proto/MessagePatchToPost>` c типом ``EditingPatches``.
- Нельзя массово подписать и отправить документы, созданные из шаблонов с настройками редактирования.
- Созданный документ можно найти среди исходящих неподписанных документов.
- Узнать, из какого шаблона был создан документ, можно с помощью свойства :doc:`../proto/Origin` в структуре :doc:`../proto/Document`.


.. _template_refuse:

Отзыв и отклонение шаблона
~~~~~~~~~~~~~~~~~~~~~~~~~~

**Отправитель** может отозвать шаблон после отправки. После отзыва получатель шаблона не сможет создать документ из шаблона, отклонить шаблон или отправить документы, созданные из шаблона до его отзыва.

**Получатель** может отклонить входящий шаблон, если он не согласен с шаблоном и не готов формировать и подписывать документ из этого шаблона. Отклонить шаблон можно только в случае, если отклонение не запрещено отправителем шаблона.

Эти действия можно осуществить с помощью метода :doc:`../http/PostTemplatePatch`. 


.. _template_other_action:

Другие действия
~~~~~~~~~~~~~~~

- Удаление шаблона — метод :doc:`../http/Delete`.
- Восстановление шаблона — метод :doc:`../http/Restore`.
- Перемещение шаблонов — метод :doc:`../http/MoveDocuments`.

Все остальные действия для шаблонов недоступны.


----

.. rubric:: См. также

*Определение:*
	- :doc:`../entities/template`

*Структуры и методы для работы с шаблонами:*
	- :doc:`../API_Templates`