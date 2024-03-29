DocflowStatus
=============

.. warning::
	Структура относится к устаревшей версии Docflow API. Используйте структуру :doc:`../../proto/DocflowStatusV3` последней версии :doc:`../../Docflow API` — V3.

.. code-block:: protobuf

    message DocflowStatus
    {
        optional DocflowStatusModel PrimaryStatus = 1;
        optional DocflowStatusModel SecondaryStatus = 2;
    }

Структура содержит информацию о статусе документооборота. В нее входит человекочитаемый текст статуса, предназначенный для вывода пользователю.

Статус формируется с точки зрения пользователя, от имени которого был сделан запрос на получение этой информации.

.. note::
	Не используйте эту структуру для построения логики обработки документов в своих интеграционных решениях. Тексты статусов пополняются новыми значениями и могут меняться. Для оценки состояния документооборота используйте поля структуры :doc:`../../proto/Docflow`.

- :doc:`PrimaryStatus <DocflowStatusModel>` — основная часть статуса.

	Примеры текстов основной части статуса: ``«Документооборот завершен»``, ``«Ожидается основная подпись. Ожидается извещение о получении»``, ``«Подписан. Требуется подписать извещение о получении»``.

-  :doc:`SecondaryStatus <DocflowStatusModel>` — второстепенная часть статуса, предназначенная для дополнительной информации.

	Примеры текстов второстепенной части статусов: ``«Аннулирование одобрено»``, ``«На согласовании»``, ``«Отказано в запросе подписи»``.
	
----

.. rubric:: Смотри также

*Структура используется:*
	- в структуре :doc:`../../proto/Docflow`.