UnsignedContent
===============

Структура данных *UnsignedContent* служит для представления подписанных ЭП данных в отправляемом сообщении.

.. code-block:: protobuf

    message UnsignedContent {
        optional bytes Content = 1;
        optional string NameOnShelf = 2;
    }


Содержит:

    :param Content: подписываемые данные (бинарное представление документа). Должно оставаться пустым (не заполняться), если заполнено поле *NameOnShelf*.

    :param NameOnShelf: имя файла с подписываемыми данными на «полке документов». Должно оставаться пустым (не заполняться), если содержимое подписанного документа размещено в поле Content.

Следует придерживаться следующей схемы использования структуры *UnsignedContent*. Если подписываемый документ имеет небольшой размер (не превышает 500Кб), его бинарное представление можно разместить непосредственно в структуре *UnsignedContent* в поле *Content*.

Если же размер документа не укладывается в эти ограничения, следует предварительно загрузить этот документ на «полку документов» при помощи серии вызовов :doc:`../http/ShelfUpload`, а затем указать имя документа на «полке» в поле *NameOnShelf* структуры *UnsignedContent*.

В противном случае сервер может отказаться обрабатывать запрос, содержащий структуры *UnsignedContent* большого размера.

Ограничения на размер передаваемых документов действуют не только на уровне отдельного документа, но и на уровне запроса к серверу.

А именно, если запрос к серверу содержит несколько документов (несколько структур *UnsignedContent*), то суммарный размер передаваемых в рамках запроса данных не должен превышать 5Мб (с учетом передаваемой служебной информации). 

Поэтому для повышения устойчивости интеграционного решения использование загрузки документов через сервис «полки документов» является рекомендуемым.