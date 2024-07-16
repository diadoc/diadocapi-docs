ParseTitleXml
=============

Метод ``ParseTitleXml`` парсит титул формализованного документа.

.. http:post:: /ParseTitleXml

	:queryparam boxId: идентификатор :doc:`ящика <../entities/box>` организации.
	:queryparam documentTypeNamedId: строковый идентификатор типа документа.
	:queryparam documentFunction: строковый идентификатор функции, уникальный в рамках типа документа.
	:queryparam documentVersion: строковый идентификатор версии, уникальный в рамках функции типа документа.
	:queryparam titleIndex: числовой идентификатор титула документа.

	:requestheader Authorization: данные, необходимые для :doc:`авторизации <../Authorization>`.

	:request Body: Тело запроса должно содержать XML-файл титула, соответствующий XSD-схеме. Получить XSD-схему титула можно с помощью метода :doc:`GetDocumentTypes` в поле ``XsdUrl``. Инструкция о получении данных из метода ``GetDocumentTypes`` приведена на странице :doc:`../instructions/getdoctypes`.

	:statuscode 200: операция успешно завершена.
	:statuscode 400: данные в запросе имеют неверный формат или отсутствуют обязательные параметры.
	:statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization`` или в этом заголовке содержатся некорректные авторизационные данные.
	:statuscode 402: у организации с указанным идентификатором ``boxId`` закончилась подписка на API.
	:statuscode 403: у пользователя нет доступа к ящику.
	:statuscode 405: используется неподходящий HTTP-метод.
	:statuscode 500: при обработке запроса возникла непредвиденная ошибка.

	:responseheader Content-Disposition: имя файла сгенерированного титула.

	:response Body: Тело ответа содержит упрощенный XML-файл, соответствующий XSD-схеме. Получить XSD-схему титула можно с помощью метода :doc:`GetDocumentTypes` в поле ``UserDataXsdUrl``. Инструкция о получении данных из метода ``GetDocumentTypes`` приведена на странице :doc:`../instructions/getdoctypes`.

Подробное описание и примеры использования метода приведены на странице :doc:`../instructions/generation`.


----

.. rubric:: См. также

*Инструкции:*
	- :doc:`../instructions/parsing`