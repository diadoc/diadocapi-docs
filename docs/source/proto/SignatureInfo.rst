SignatureInfo
======================

.. code-block:: protobuf

   message SignatureInfo 
	{
		required Timestamp SigningTime = 1;
		optional Timestamp SignatureVerificationTime = 2;
		optional SignatureVerificationResult SignatureVerificationResult = 3;
		required string Thumbprint = 4;
		required string SerialNumber = 5;
		optional string Issuer = 6;
		optional string StartDate = 7;
		optional string EndDate = 8;
		optional string OrgName = 9;
		optional string OrgInn = 10;
		optional string JobTitle = 11;
		optional string FirstName = 12;
		optional string Surname = 13;
		optional string Snils = 14;
		optional string Email = 15;
	}

Структура представляет информацию о подписи и сертификате. 

-  :doc:`SigningTime <Timestamp>` - время формирования подписи.
-  :doc:`SignatureVerificationTime <Timestamp>` - дата проверки подписи.
-  :doc:`SignatureVerificationResult <SignatureVerificationResult>` - результат проверки подписи.
-  *Thumbprint* - отпечаток сертификата.
-  *SerialNumber* - серийный номер.
-  *Issuer* - кем выдан сертификат.
-  *StartDate* - дата начала действия сертификата.
-  *EndDate* - дата окончания действия сертификата.
-  *OrgName* - наименование организации.
-  *OrgInn* - ИНН организации.
-  *JobTitle* - должность владельца сертификата.
-  *FirstName* - имя и отчество (либо имя, если не указано отчество) владельца сертификата.
-  *Surname* - фамилия владельца сертификата.
-  *Snils* - СНИЛС владельца сертификата.
-  *Email* - электронная почта владельца сертификата.
