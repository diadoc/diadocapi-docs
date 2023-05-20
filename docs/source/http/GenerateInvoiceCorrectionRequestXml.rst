GenerateInvoiceCorrectionRequestXml
===================================

Метод ``GenerateInvoiceCorrectionRequestXml`` генерирует xml-файл уведомления об уточнении счета-фактуры.

Версии метода:

	- :ref:`GenerateInvoiceCorrectionRequestXml V2 <GenerateInvoiceCorrectionRequestXml_v2>`.
	- :ref:`GenerateInvoiceCorrectionRequestXml <GenerateInvoiceCorrectionRequestXml_v1>` — устаревшая версия. Не поддерживает заполнение всех полей уведомления об уточнении формата, утвержденного приказом `№ ЕД-7-26/133@ <https://www.nalog.gov.ru/rn77/about_fts/docs/13194601/>`__.

.. _GenerateInvoiceCorrectionRequestXml_v2:

GenerateInvoiceCorrectionRequestXml V2
--------------------------------------

.. http:post:: /V2/GenerateSignatureRejectionXml

	:queryparam boxId: идентификатор ящика организации.

	:requestheader Authorization: данные, необходимые для :doc:`авторизации <../Authorization>`.

	:request Body: Тело запроса должно содержать структуру :doc:`../proto/InvoiceCorrectionRequestGenerationRequestV2`.
	
	:statuscode 200: операция успешно завершена.
	:statuscode 400: данные в запросе имеют неверный формат или отсутствуют обязательные параметры.
	:statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization`` или в этом заголовке содержатся некорректные авторизационные данные.
	:statuscode 402: у организации с указанным идентификатором ``boxId`` закончилась подписка на API.
	:statuscode 403: доступ к ящику с предоставленным авторизационным токеном запрещен.
	:statuscode 404: в указанном ящике нет сообщения с идентификатором ``messageId`` или в указанном сообщении нет сущности с идентификатором ``attachmentId``, или указанная сущность имеет неверный тип, или у указанной сущности нет дочерней сущности типа :doc:`../proto/Signature`
	:statuscode 405: используется неподходящий HTTP-метод.
	:statuscode 409: невозможно сформировать уведомление об уточнении.
	:statuscode 500: при обработке запроса возникла непредвиденная ошибка.

	:responseheader Content-Disposition: имя файла с уведомлением.
	
	:response Body: Тело ответа содержит XML-файл уведомления об уточнении счета-фактуры (ИСФ/КСФ/ИКСФ) ``attachmentId`` из сообщения ``messageId`` в ящике ``boxId``. Файл формируется в соответствии с :download:`XSD-схемой <../xsd/DP_UVUTOCH_1_985_00_01_03_01.xsd>`.

Для выполнения метода текущий пользователь должен иметь доступ к документу исходного счета-фактуры, иначе метод вернет ошибку ``403 (Forbidden)``.

.. _GenerateInvoiceCorrectionRequestXml_v1:

GenerateInvoiceCorrectionRequestXml
-----------------------------------

.. http:post:: /V2/GenerateSignatureRejectionXml

	:queryparam boxId: идентификатор ящика организации.
	:queryparam messageId: идентификатор сообщения.
	:queryparam attachmentId: идентификатор сущности СФ/ИСФ/КСФ/ИКСФ, для которой нужно сформировать уведомление об уточнении.

	:requestheader Authorization: данные, необходимые для :doc:`авторизации <../Authorization>`.

	:request Body: Тело запроса должно содержать данные для формирования уведомления об уточнении в виде сериализованной структуры :doc:`../proto/InvoiceCorrectionRequestInfo`.
	
	:statuscode 200: операция успешно завершена.
	:statuscode 400: данные в запросе имеют неверный формат или отсутствуют обязательные параметры.
	:statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization`` или в этом заголовке содержатся некорректные авторизационные данные.
	:statuscode 402: у организации с указанным идентификатором ``boxId`` закончилась подписка на API.
	:statuscode 403: доступ к ящику с предоставленным авторизационным токеном запрещен.
	:statuscode 404: в указанном ящике нет сообщения с идентификатором ``messageId`` или в указанном сообщении нет сущности с идентификатором ``attachmentId``, или указанная сущность имеет неверный тип, или у указанной сущности нет дочерней сущности типа :doc:`../proto/Signature`
	:statuscode 405: используется неподходящий HTTP-метод.
	:statuscode 409: невозможно сформировать уведомление об уточнении.
	:statuscode 500: при обработке запроса возникла непредвиденная ошибка.

	:responseheader Content-Disposition: имя файла с уведомлением.
	
	:response Body: Тело ответа содержит XML-файл уведомлениея об уточнении счета-фактуры (ИСФ/КСФ/ИКСФ) ``attachmentId`` из сообщения ``messageId`` в ящике ``boxId``. Файл формируется в соответствии с :download:`XML-схемой <../xsd/DP_UVUTOCH_1_985_00_01_02_02.xsd>`.

Для выполнения метода текущий пользователь должен иметь доступ к документу исходного счета-фактуры, иначе метод вернет ошибку ``403 (Forbidden)``.