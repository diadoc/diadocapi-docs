Другие функции
==============

.. contents:: :local:

Отправка заявления участника ЭДО
--------------------------------

Отправить заявление участника электронного документооборота можно с помощью метода :doc:`http/SendFnsRegistrationMessage`.

Подготовка печатных форм
------------------------

Документы, которые передаются через Диадок в формализованном виде, выглядят как XML-файл и имеют нечитаемый вид.
Диадок позволяет получить печатную форму для таких документов, чтобы отобразить их пользователю в удобном формате.

В первую очередь эта функциональность предназначена для формирования печатных форм счетов-фактур, универсальных передаточных документов, накладных и актов о выполненных работах, предусмотренных порядком Минфина.

Печатные формы документов можно получить с помощью метода :doc:`http/GeneratePrintForm`.

.. _autoregistration:

Авторегистрация
---------------

**Авторегистрация** — это автоматическое создание в Диадоке сотрудника организации с правами администратора. Сотрудник будет создан, если пользователь имеет сертификат КЭП организации.

Сотрудник с правами администратора будет автоматически создан в организации, если выполняется хотя бы одно из условий:

	- В организации нет администраторов с подтвержденной учетной записью и действующим сертификатом.
	- В организации есть администратор с таким же СНИЛС, как в сертификате.
	- В сертификате указана одна из должностей: главный бухгалтер, генеральный директор, директор, главный врач, ректор.

Сотрудник не будет автоматически создан в организации, если:

	- Запрос пользователя на доступ в ящик раньше отклоняли.
	- Пользователя удаляли из организации.
	- Организация является частью филиальной структуры.
	- Сертификат выдан представительству/филиалу иностранной организации — ИНН начинается с “99”.
	- Сертификат выдан физическому лицу.

Зарегистрировать сотрудника можно с помощью следующих методов:

	- :doc:`../http/GetMyOrganizations`,
	- :doc:`../http/Register`,
	- любой метод, в котором есть идентификатор ящика ``boxId``. Если условия для авторегистрации не выполняются, метод вернет ошибку ``403 (Forbidden)``. Если в организации есть действующий администратор, то при вызове метода будет отправлен запрос на доступ к ящику. В этом случае метод вернет ошибку ``403 (Forbidden)`` с текстом ``Access to Box is denied. Request to admins of Box was created. Please try again later``.


.. _editing_settings:

Настройки редактирования
------------------------

Настройки редактирования дают возможность создать документ, который можно будет отредактировать перед отправкой. 

Настройки редактирования «ослабляют» требования к документу и позволяют отправить его с незаполненными полями. Незаполнены могут быть даже обязательные поля формализованного документа, например, номер документа. Такой документ нужно дозаполнить перед отправкой. Кроме этого настройки редактирования позволяют создать документ с заполенными полями, которые можно отредактировать перед отправкой.

Не все поля документа можно сделать редактируемыми. Диадок позволяет создать редактируемые документы со следующими типами и полями:

.. table:: Настройки редактирования

	+---------------------------------+-------------------------------------------------------------------------+
	| Тип документа                   | Редактируемые поля                                                      |
	+=================================+=========================================================================+
	| УПД                             | - Номер документа                                                       |
	|                                 | - Номер + дата документа                                                |
	|                                 | - Номер документа + упрощенные банковские реквизиты                     |
	|                                 | - Номер + дата документа + упрощенные банковские реквизиты              |
	|                                 | - Номер + дата документа + расширенные банковские реквизиты             |
	|                                 | - Номер документа + строка 5А                                           |
	|                                 | - Номер + дата документа + строка 5А                                    |
	|                                 | - Номер документа + упрощенные банковские реквизиты + строка 5А         |
	|                                 | - Номер + дата документа + упрощенные банковские реквизиты + строка 5А  |
	|                                 | - Номер + дата документа + расширенные банковские реквизиты + строка 5А |
	|                                 | - Маркировка                                                            |
	+---------------------------------+-------------------------------------------------------------------------+
	| Приложение к УПД                | - Номер документа                                                       |
	+---------------------------------+-------------------------------------------------------------------------+
	| Показания электроэнергии        | - Показания счетчика новое                                              |
	|                                 | - Дополнительный расход электроэнергии                                  |
	+---------------------------------+-------------------------------------------------------------------------+
	| Поручение экспедитору           | - Данные о водителе                                                     |
	|                                 | - Данные о транспортном средстве                                        |
	+---------------------------------+-------------------------------------------------------------------------+
	| Заявка на перевозку             | - Данные о водителе                                                     |
	|                                 | - Данные о транспортном средстве                                        |
	+---------------------------------+-------------------------------------------------------------------------+
	| Заявка на оказание транспортно- | - Данные о водителе                                                     |
	| экспедиционных услуг            | - Данные о транспортном средстве                                        |
	+---------------------------------+-------------------------------------------------------------------------+

	
Для каждого из перечисленных в таблице типа документа и его набора полей существует собственный уникальный идентификатор настройки редактирования. Чтобы получить идентификатор настройки редактирования для конкретного набора полей документа, обратитесь к вашему менеджеру или в `техническую поддержку <https://www.diadoc.ru/support>`__.

Указать настройки редактирования можно только для :doc:`шаблона <entities/template>` или документа с :ref:`отложенной отправкой <doc_delaysend>`. Для этого используйте следующие методы:

	- :doc:`http/PostTemplate` — для шаблона; чтобы заполнить настройки редактирования, следуйте :ref:`инструкции <template_editing>`.
	- :doc:`http/PostMessage` с параметром ``DelaySend`` — для исходящего неотправленного документа; укажите идентификатор настройки редактирования в поле ``EditingSettingId`` структуры :doc:`proto/DocumentAttachment`.

Добавление метки технологического партнера
------------------------------------------

При вызове методов API вы можете указать свою метку технологического партнера.

Чтобы указать метку технологического партнера, нужно при вызове каждого метода API добавлять в него заголовок ``X-Solution-Info``. В качестве значения заголовка передайте строку, содержащую вашу метку технологического партнера, например:

::

    X-Solution-Info: SoftwareName
	
..