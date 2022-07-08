GetCounteragentCertificates
===========================

Метод ``GetCounteragentCertificates`` возвращает сертификаты контрагента.

.. http:get:: /GetCounteragentCertificates

	:queryparam myOrgId: идентификатор организации, от лица которой будет произведен поиск сертификатов контрагента.
	:queryparam counteragentOrgId: идентификатор организации, у которой осуществляется поиск сертификатов контрагента.
	
	:requestheader Authorization: данные, необходимые для :doc:`авторизации <../Authorization>`.
	
	:statuscode 200: операция успешно завершена.
	:statuscode 400: данные в запросе имеют неверный формат или отсутствуют обязательные параметры.
	:statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization`` или в этом заголовке содержатся некорректные авторизационные данные.
	:statuscode 402: у организации с указанным идентификатором ``myOrgId`` закончилась подписка на API.
	:statuscode 403: доступ к списку сертификатов организации ``counteragentOrgId`` от организации ``myOrgId`` с предоставленным авторизационным токеном запрещен.
	:statuscode 404: партнерские отношения между организациями ``myOrgId`` и ``counteragentOrgId`` не установлены.
	:statuscode 405: используется неподходящий HTTP-метод.
	:statuscode 500: при обработке запроса возникла непредвиденная ошибка.
	
Метод возвращает информацию о сертификатах контрагента ``counteragentOrgId``, представленную структурой :doc:`CounteragentCertificateList <../proto/Counteragent>`.

Организация имеет право запрашивать список сертификатов контрагента ``counteragentOrgId``, если у нее включена возможность отправки зашифрованных документов. Эта возможность указана в поле :doc:`Organization.Box.EncryptedDocumentsAllowed <../proto/Box>`.