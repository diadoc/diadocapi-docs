DetectCustomPrintForms
======================

.. http:post:: /DetectCustomPrintForms

	:queryparam boxId: идентификатор ящика организации.

	:requestheader Authorization: данные, необходимые для :doc:`авторизации <../Authorization>`.

	:request Body: Тело запроса должно содержать структуру :ref:`CustomPrintFormDetectionRequest`.

	:statuscode 200: операция успешно завершена.
	:statuscode 400: данные в запросе имеют неверный формат или отсутствуют обязательные параметры.
	:statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization`` или в этом заголовке содержатся некорректные авторизационные данные.
	:statuscode 403: доступ к ящику с предоставленным авторизационным токеном запрещен или у пользователя нет доступа к каким-то документам из запроса.
	:statuscode 405: используется неподходящий HTTP-метод.
	:statuscode 500: при обработке запроса возникла непредвиденная ошибка.

Метод возвращает структуру :ref:`CustomPrintFormDetectionResult`.

Метод позволяет по списку документов определить, есть ли у документов нестандартная печатная форма. Скачать печатную форму документа можно при помощи метода :doc:`../http/GeneratePrintForm`.

Максимальное количество документов в списке на один запрос — 100.

.. _CustomPrintFormDetectionRequest:

CustomPrintFormDetectionRequest
-------------------------------

.. code-block:: protobuf

    message CustomPrintFormDetectionRequest {
        repeated DocumentId DocumentIds = 1;
    }

Структура данных *CustomPrintFormDetectionRequest* содержит список документов, для которых необходимо определить наличие нестандартной печатной формы.

- :doc:`../proto/DocumentId` — идентификатор документа

.. _CustomPrintFormDetectionResult:

CustomPrintFormDetectionResult
------------------------------

.. code-block:: protobuf

    message CustomPrintFormDetectionResult {
       repeated CustomPrintFormDetectionItemResult Items = 1;
    }

    message CustomPrintFormDetectionItemResult {
       required DocumentId DocumentId = 1;
       required bool HasCustomPrintForm = 2;
    }

Структура данных *CustomPrintFormDetectionResult* содержит результат проверки.

- :doc:`../proto/DocumentId` — идентификатор документа
- *HasCustomPrintForm* — флаг, показывающий, что данный документ имеет нестандартную печатную форму
