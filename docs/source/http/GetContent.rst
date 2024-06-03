GetContent
==========

Метод ``GetContent`` возвращает XSD-схему документа.

.. http:get:: /GetContent

	:queryparam typeNamedId: идентификатор типа документа.
	:queryparam function: функция документа.
	:queryparam version: версия документа.
	:queryparam titleIndex: числовой идентификатор титула документа.
	:queryparam contentType: тип контента.

	:requestheader Authorization: данные, необходимые для :doc:`авторизации <../Authorization>`.

	:statuscode 200: операция успешно завершена.
	:statuscode 400: данные в запросе имеют неверный формат или отсутствуют обязательные параметры.
	:statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization`` или в этом заголовке содержатся некорректные авторизационные данные.
	:statuscode 405: используется неподходящий HTTP-метод.
	:statuscode 500: при обработке запроса возникла непредвиденная ошибка.

	:response Body: Тело ответа содержит XSD-схему документа.

Получить параметры можно с помощью метода :doc:`../http/GetDocumentTypes`. Инструкция о получении данных из метода ``GetDocumentTypes`` приведена на странице :doc:`../instructions/getdoctypes`. В ответе метод вернет URL-пути в полях:

	- ``XsdUrl``— URL-путь метода, возвращающего файл XSD-схемы титула;
	- ``UserDataXsdUrl`` — URL-путь метода, возвращающего файл XSD-схемы контракта для генерации титула с помощью обобщённого метода генерации;
	- ``SignerUserDataXsdUrl`` — URL-путь метода, возвращающего файл упрощенной XSD-схемы подписанта.






