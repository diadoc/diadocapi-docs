DetectCustomPrintForms
======================

Метод ``DetectCustomPrintForms`` выявляет нестандартную печатную форму у документов из списка.

Получить печатную форму документа можно с помощью метода :doc:`../http/GeneratePrintForm`.

.. http:post:: /DetectCustomPrintForms

	:queryparam boxId: идентификатор ящика организации.

	:requestheader Authorization: данные, необходимые для :doc:`авторизации <../Authorization>`.

	:request Body: Тело запроса должно содержать структуру ``CustomPrintFormDetectionRequest``, содержащую список документов, для которых нужно определить наличие нестандартной печатной формы:
	
		.. code-block:: protobuf

			message CustomPrintFormDetectionRequest {
				repeated DocumentId DocumentIds = 1;
			}

		..
	
		- ``DocumentIds`` — список идентификаторов документов, представленных структурой :doc:`../proto/DocumentId`.

	:statuscode 200: операция успешно завершена.
	:statuscode 400: данные в запросе имеют неверный формат или отсутствуют обязательные параметры.
	:statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization`` или в этом заголовке содержатся некорректные авторизационные данные.
	:statuscode 403: доступ к ящику с предоставленным авторизационным токеном запрещен или у пользователя нет доступа к каким-то документам из запроса.
	:statuscode 405: используется неподходящий HTTP-метод.
	:statuscode 500: при обработке запроса возникла непредвиденная ошибка.

Метод возвращает структуру ``CustomPrintFormDetectionResult``, содержащую результаты проверки:

.. code-block:: protobuf

    message CustomPrintFormDetectionResult {
       repeated CustomPrintFormDetectionItemResult Items = 1;
    }

    message CustomPrintFormDetectionItemResult {
       required DocumentId DocumentId = 1;
       required bool HasCustomPrintForm = 2;
    }

- ``Items`` — список результатов проверки, представленных структурой ``CustomPrintFormDetectionItemResult`` с полями:

	- ``DocumentId`` — идентификатор документа, представленный структурой :doc:`../proto/DocumentId`.
	- ``HasCustomPrintForm`` — флаг, показывающий, что данный документ имеет нестандартную печатную форму.

Метод обрабатывает за один запрос не более 100 документов.