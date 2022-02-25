DocflowStatusV3
===============

Структура ``DocflowStatusV3`` содержит информацию о статусе документооборота. В нее входит человекочитаемый текст статуса, предназначенный для вывода пользователю.

.. code-block:: protobuf

   message DocflowStatusV3
   {
        required DocflowStatusModelV3 PrimaryStatus = 1;
        optional DocflowStatusModelV3 SecondaryStatus = 2;
        optional PowerOfAttorneyValidationStatus PowerOfAttorneyGeneralStatus = 3;
   }

Статус формируется с точки зрения пользователя, от имени которого был сделан запрос на получение этой информации.

.. note::
	Не используйте эту структуру для построения логики обработки документов в своих интеграционных решениях. Тексты статусов пополняются новыми значениями и могут меняться. Для оценки состояния документооборота используйте поля структуры :doc:`DocflowV3`.

- ``PrimaryStatus`` — основная часть статуса, представленная структурой :doc:`DocflowStatusModelV3`.
 Примеры текстов основной части статуса: ``«Документооборот завершен»``, ``«Ожидается основная подпись. Ожидается извещение о получении»``, ``«Подписан. Требуется подписать извещение о получении»``.

- ``SecondaryStatus`` — второстепенная часть статуса, предназначенная для дополнительной информации, представленная структурой :doc:`DocflowStatusModelV3`.
 Примеры текстов второстепенной части статусов: ``«Аннулирование одобрено»``, ``«На согласовании»``, ``«Отказано в запросе подписи»``.

- ``PowerOfAttorneyGeneralStatus`` — информация о сводном статусе по всем машиночитаемым доверенностям (МЧД), представленная структурой :doc:`PowerOfAttorneyValidationStatus`.
 Сводный статус формируется на основании всех МЧД, которые были приложены к документу при совершении действий с ним, например: подписание, ИоП, аннулирование, согласующая подпись и т.п. Сводный статус формируется по следующим правилам:
 
	- если среди МЧД есть хотя бы одна невалидная, то ``StatusNamedId=IsNotValid``;
	- если не получилось выполнить проверку из-за ошибки валидации МЧД, то ``StatusNamedId=CanNotBeValidated``;
	- если при проверке возникли ошибки валидации МЧД, то ``StatusNamedId=ValidationError``;
	- если все проверки выполнены без ошибок, то ``StatusNamedId=IsValid``.

----

.. rubric:: Использование

Структура ``DocflowStatusV3`` используется внутри структур:

- :doc:`DocflowV3`, возвращается методами :doc:`V3/GetDocflowEvents <../http/GetDocflowEvents_V3>`, :doc:`V3/GetDocflows <../http/GetDocflows_V3>`, :doc:`V3/GetDocflowsByPacketId <../http/GetDocflowsByPacketId_V3>`, :doc:`V3/SearchDocflows <../http/SearchDocflows_V3>`
- :doc:`Document`, возвращается методами :doc:`../http/GetDocument`, :doc:`../http/GetDocuments`, :doc:`../http/GetDocumentsByMessageId`