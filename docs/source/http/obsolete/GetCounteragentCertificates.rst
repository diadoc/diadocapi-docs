GetCounteragentCertificates
===========================

.. warning::
	Эта версия метода устарела. Используйте новую версию метода :doc:`../GetCounteragentCertificates`.

Метод ``GetCounteragentCertificates`` возвращает :doc:`сертификаты <../../entities/certificate>` :doc:`контрагента <../../entities/counteragent>`.

.. http:get:: /GetCounteragentCertificates

	:queryparam myOrgId: идентификатор организации, от лица которой будет произведен поиск сертификатов контрагента.
	:queryparam counteragentOrgId: идентификатор организации, у которой осуществляется поиск сертификатов контрагента.
	
	:requestheader Authorization: данные, необходимые для :doc:`авторизации <../../Authorization>`.
	
	:statuscode 200: операция успешно завершена.
	:statuscode 400: данные в запросе имеют неверный формат или отсутствуют обязательные параметры.
	:statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization`` или в этом заголовке содержатся некорректные авторизационные данные.
	:statuscode 402: у организации с указанным идентификатором ``myOrgId`` закончилась подписка на API.
	:statuscode 403: доступ к списку сертификатов организации ``counteragentOrgId`` от организации ``myOrgId`` с предоставленным авторизационным токеном запрещен.
	:statuscode 404: партнерские отношения между организациями ``myOrgId`` и ``counteragentOrgId`` не установлены.
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

.. include:: ../../include/accessMethod_required_box.txt

Организация имеет право запрашивать список сертификатов контрагента ``counteragentOrgId``, если у нее включена возможность отправки зашифрованных документов. Эта возможность указана в поле :doc:`Organization.Box.EncryptedDocumentsAllowed <../../proto/Box>`.