CloudSignConfirm
================

Метод ``CloudSignConfirm`` подтверждает операцию подписания Контур.Сертификатом с помощью смс-кода.

.. http:post:: /CloudSignConfirm

	:queryparam token: идентификатор операции подписания Контур.Сертификатом, полученный в результате вызова пары методов :doc:`CloudSign` и :doc:`CloudSignResult`.
	:queryparam confirmationCode: смс-код подтверждения операции подписания Контур.Сертификатом.
	:queryparam locationPreference: способ, которым нужно вернуть результат подписания. Может принимать значения:

		- ``Content`` — байтовое представление, значение по умолчанию.
		- ``Reference`` — путь на полке. Подробно про загрузку на полку в описании метода :doc:`ShelfUpload`.

	:requestheader Authorization: данные, необходимые для :doc:`авторизации <../Authorization>`.

	:statuscode 200: операция успешно завершена.
	:statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization`` или в этом заголовке содержатся некорректные авторизационные данные.
	:statuscode 405: используется неподходящий HTTP-метод.
	:statuscode 409: зависит от значения заголовка ``X-Diadoc-ErrorCode``:

		- ``CloudCrypt.BadConfirmationCode`` — указан неверный код подтверждения;
		- ``CloudCrypt.ExpiredRequest`` — истек срок действия кода подтверждения.
	
	:responseheader X-Diadoc-ErrorCode: текст ошибки.

	:statuscode 500: при обработке запроса возникла непредвиденная ошибка.

	:response Body: Тело ответа содержит идентификатор операции ``taskId`` в структуре :doc:`../proto/AsyncMethodResult`. По этому идентификатору с помощью метода :doc:`CloudSignConfirmResult` можно узнать результат обработки запроса.

----

.. rubric:: Смотри также

*Другие методы для работы с Контур.Сертификатом:*
	- :doc:`CloudSignConfirmResult` — возвращает подписи, созданные с использованием Контур.Сертификата.
	- :doc:`CloudSign` — начинает асинхронную операцию подписания данных.
	- :doc:`CloudSignResult` — завершает операцию подписания данных.