GetGeneratedPrintForm
=====================

Метод ``GetGeneratedPrintForm`` генерирует печатную форму документа по идентификатору, полученному методом :doc:`GeneratePrintFormFromAttachment`.

.. http:get:: /GetGeneratedPrintForm

	:queryparam printFormId: идентификатор печатной формы, полученный с помощью метода :doc:`GeneratePrintFormFromAttachment`.

	:requestheader Authorization: данные, необходимые для :doc:`авторизации <../Authorization>`.

	:statuscode 200: операция успешно завершена.
	:statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization`` или в этом заголовке содержатся некорректные авторизационные данные.
	:statuscode 409: по ``printFormId`` не найдена печатная форма. Повторно вызовите метод :doc:`GeneratePrintFormFromAttachment`.
	:statuscode 500: при обработке запроса возникла непредвиденная ошибка.

	:responseheader Retry-After: если в ответе содержится HTTP-заголовок ``Retry-After``, то предыдущий вызов этого метода с таким же идентификатором операции еще не завершен. В этом случае следует повторить вызов через указанное в заголовке время (в секундах), чтобы убедиться, что операция завершилась без ошибок.

	:response Body: Тело ответа содержит файл сгенерированной печатной формы документа.

----

.. rubric:: См. также

.. include:: ../reused_text/printform_seealso.txt