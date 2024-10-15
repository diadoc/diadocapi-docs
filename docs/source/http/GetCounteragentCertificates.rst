GetCounteragentCertificates
===========================

Метод ``GetCounteragentCertificates`` возвращает :doc:`сертификаты <../entities/certificate>` :doc:`контрагента <../entities/counteragent>`.

.. http:get:: /V2/GetCounteragentCertificates

	:queryparam myBoxId: идентификатор :doc:`ящика <../../entities/box>` организации, от лица которой будет произведен поиск сертификатов контрагента.
	:queryparam counteragentBoxId: идентификатор :doc:`ящика <../../entities/box>` организации контрагента, у которой осуществляется поиск сертификатов контрагента.

	:requestheader Authorization: данные, необходимые для :doc:`авторизации <../Authorization>`.

	:statuscode 200: операция успешно завершена.
	:statuscode 400: данные в запросе имеют неверный формат или отсутствуют обязательные параметры.
	:statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization`` или в этом заголовке содержатся некорректные авторизационные данные.
	:statuscode 402: у организации с указанным идентификатором ``myBoxId`` закончилась подписка на API.
	:statuscode 403: доступ к списку сертификатов организации ``counteragentBoxId`` от организации ``myBoxId`` с предоставленным авторизационным токеном запрещен.
	:statuscode 404: партнерские отношения между организациями ``myBoxId`` и ``counteragentBoxId`` не установлены.
	:statuscode 405: используется неподходящий HTTP-метод.
	:statuscode 500: при обработке запроса возникла непредвиденная ошибка.

	:response Body: Тело ответа содержит структуру ``CounteragentCertificateList``:

		.. code-block:: protobuf

		    message CounteragentCertificateList {
		        repeated Certificate Certificates = 1;
		    }

		    message Certificate {
		        required bytes RawCertificateData = 1;
		    }

		- ``Certificates`` — список сертификатов контрагента. Каждый элемент списка представлен структурой ``Certificate`` с полями:

			- ``RawCertificateData`` — сертификат, сериализованный в массив байтов в DER-кодировке.

.. include:: ../include/accessMethod_required_box.txt

.. include:: ../include/access_required_encryptedDocumentsAllowed.txt


Примеры использования
---------------------

**Пример HTTP-запроса:**

.. literalinclude:: ../include/getCounteragentCertificates_query.txt

**Пример тела ответа:**

.. literalinclude:: ../include/getCounteragentCertificates_resp.txt
	:language: json


----

.. rubric:: См. также

.. include:: ../include/seealso_method_counteragent.txt

*Устаревшие версии метода:*
	- :doc:`obsolete/GetCounteragentCertificates`