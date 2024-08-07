DocflowStatus
=============

.. warning::
	Структура устарела. Вместо нее используется структура :doc:`../DocflowStatusV3`.

Структура ``DocflowStatus`` содержит информацию о статусе документооборота. Включает в себя человекочитаемый текст статуса, предназначенный для вывода пользователю.

Статус формируется с точки зрения пользователя, от имени которого был сделан запрос на получение этой информации.

.. note::
	Не используйте эту структуру для построения логики обработки документов в своих интеграционных решениях. Тексты статусов пополняются новыми значениями и могут меняться. Для оценки состояния документооборота используйте поля структуры :doc:`Docflow`.

.. code-block:: protobuf

    message DocflowStatus
    {
        optional DocflowStatusModel PrimaryStatus = 1;
        optional DocflowStatusModel SecondaryStatus = 2;
    }

- ``PrimaryStatus`` — основная часть статуса, представленная структурой :doc:`DocflowStatusModel`.

   Примеры текстов основной части статуса: ``«Документооборот завершен»``, ``«Ожидается основная подпись. Ожидается извещение о получении»``, ``«Подписан. Требуется подписать извещение о получении»``.

- ``SecondaryStatus`` — второстепенная часть статуса, предназначенная для дополнительной информации. Представлена структурой :doc:`DocflowStatusModel`

   Примеры текстов второстепенной части статусов: ``«Аннулирование одобрено»``, ``«На согласовании»``, ``«Отказано в запросе подписи»``.


----

.. rubric:: См. также

*Структура используется:*
	- в устаревшей структуре :doc:`Docflow`