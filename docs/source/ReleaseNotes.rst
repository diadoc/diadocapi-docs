История изменений API
=====================

28.03.2022
----------
**SDK**: `Java 3.9.9 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions%2F3.9.9>`__

- В Java SDK реализована функциональность для :doc:`работы с машиночитаемой доверенностью <howto/powerofattorney>`.


23.02.2022
----------
**SDK**: `C# 2.9.29 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions%2F2.9.29>`__ | `Java 3.9.9 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions%2F3.9.9>`__ | `C++ 1.92.9 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/versions%2F1.92.9>`__

- Изменена структура :doc:`CounteragentList <proto/Counteragent>`: добавлено поле ``CounteragentList.TotalCountType``, которое отражает количество контрагентов, возвращаемых в поле ``TotalCount``. Для поля ``TotalCount`` введено ограничение значения: теперь в нем возвращает значение не больше 10000. Это ограничение введено для повышения производительности метода поиска контрагентов.


21.02.2022
----------
**SDK**: `C# 2.9.28 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions%2F2.9.28>`__

- API Диадока теперь поддерживает :doc:`работу с машиночитаемой доверенностью <howto/powerofattorney>` (МЧД).

- Реализованы методы для работы с машиночитаемой доверенностью.

	- Регистрация МЧД:
	
		- методы :doc:`http/RegisterPowerOfAttorney` и :doc:`http/RegisterPowerOfAttorneyResult` для регистрации МЧД.
		
	- Работа с МЧД сотрудника:
	
		- метод :doc:`http/AddEmployeePowerOfAttorney` для привязки МЧД к сотруднику.
		- метод :doc:`http/DeleteEmployeePowerOfAttorney` для отвязки МЧД от сотрудника.
		- метод :doc:`http/UpdateEmployeePowerOfAttorney` для обновления настроек МЧД сотрудника.
		- метод :doc:`http/GetEmployeePowersOfAttorney` для получения всх МЧД сотрудника.
		
	- Получение и проверка МЧД:
	
		- метод :doc:`http/GetPowerOfAttorneyInfo` для получения информации о МЧД, отправленной с документом.
		- метод :doc:`http/PrevalidatePowerOfAttorney` для предварительной проверки МЧД.

- Реализована отправка документов с машиночитаемой доверенностью (МЧД).

 При отправке документов методами :doc:`http/PostMessage`, :doc:`http/PostMessagePatch` и :doc:`http/SendDraft` теперь можно указать МЧД. Для этого изменены структуры :doc:`proto/SignedContent`, :doc:`proto/DocumentSignature` и :doc:`proto/DocumentSenderSignature`, которые теперь могут хранить информацию о МЧД в новой структуре :doc:`proto/PowerOfAttorneyToPost`.

- Реализовано получение машиночитаемой доверенности (МЧД).

	- Получение МЧД в сообщении.

	 В методы :doc:`http/GetMessage`, :doc:`http/GetNewEvents`, :doc:`http/GetLastEvent` и :doc:`http/GetEvent` добавлена возможность получить информацию о МЧД и ее статусе. Для этого реализована структура :doc:`proto/PowerOfAttorneyInfo`, используемая в структуре :doc:`proto/Entity message`.
	 В перечисление ``AttachmentType`` добавлены значения:

		- ``PowerOfAttorney`` — информация о МЧД
		- ``PowerOfAttorneyStatus`` — статус проверки МЧД

	- Получение МЧД в docflow.

	 В методах :doc:`V3/GetDocflowEvents <../http/GetDocflowEvents_V3>`, :doc:`V3/GetDocflows <../http/GetDocflows_V3>`, :doc:`V3/GetDocflowsByPacketId <../http/GetDocflowsByPacketId_V3>`, :doc:`V3/SearchDocflows <../http/SearchDocflows_V3>` реализованы следующие изменения:

		- добавлена возможность получить информацию об общем (сводном) статусе по всем МЧД для всех сущностей документа. Для этого изменена структура :doc:`proto/DocflowStatusV3`, которая теперь содержит новую структуру :doc:`proto/PowerOfAttorneyValidationStatus`, хранящую информацию о сводном статусе МЧД.
		- добавлена возможность получить информацию о МЧД и ее статусе из подписи под документом. Для этого изменена структура :doc:`proto/SignatureV3`, которая теперь хранит информацию о подписи с использованием МЧД в своей структуре :doc:`proto/SignaturePowerOfAttorney`.

	- Получение МЧД в документах.

	 Методы :doc:`http/GetDocument`, :doc:`http/GetDocuments`, :doc:`http/GetDocumentsByMessageId` теперь возвращают информацию об общем (сводном) статусе по всем МЧД для всех сущностей документа. Для этого изменена структура :doc:`proto/DocflowStatusV3` в структуре :doc:`proto/Document`, которая теперь содержит новую структуру :doc:`proto/PowerOfAttorneyValidationStatus`, хранящую информацию о сводном статусе МЧД.
	 
- Реализована генерция титулов с машиночитаемой доверенностью (МЧД).

 Метод :doc:`http/GenerateTitleXml` теперь может генерировать :ref:`титулы с МЧД <generate_title_xml_poa>`.
 
- Реализована подготовка к подписанию документа с машиночитаемой доверенностью (МЧД).
 
 Метод :doc:`http/PrepareDocumentsToSign` теперь может подготовить к подписанию документ с МЧД. Для этого в структуру :doc:`proto/utd/ExtendedSigner` включена структура :doc:`proto/PowerOfAttorneyToPost`, содержащая данные о МЧД.


26.01.2022
----------
**SDK**: `C# 2.9.23 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions%2F2.9.23>`__

- Внесены изменения для работы с подтверждениями роумингового оператора:

 - Добавлен новый тип вложения :doc:`AttachmentType <proto/Entity message>` — ``RoamingConfirmation``. Он представляет собой подтверждение оператора, отправленное в роуминг или полученное из роуминга.
 - В структуру :doc:`proto/ConfirmationDocflow` добавлено новое поле ``RoamingConfirmation``. Оно содержит подтверждение оператора, отправленное в роуминг или полученное из роуминга, представленное структурой :doc:`OperatorConfirmationDocflow`.


06.10.2021
----------
**SDK**: `C# 2.9.22 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions%2F2.9.22>`__ | `Java 3.9.8 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions%2F3.9.8>`__ | `C++ 1.92.8 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/versions%2F1.92.8>`__

- Добавлена новая версия метода :doc:`/V2/GenerateRevocationRequestXml <http/GenerateRevocationRequestXml>`. Метод позволяет сгенерировать предложение об аннулировании версии 1.02. Если получатель ПоА в роуминге, то метод сгенерирует ту версию, которую поддерживает оператор.


05.10.2021
----------
**SDK**: `C# 2.9.21 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions%2F2.9.21>`__

- В структуру :doc:`http/utd/ExtendedSignerDetailsV2` добавлено значение ``Ucd736Buyer``  для поддержки формата приказа №736.


20.09.2021
----------
**SDK**: `C# 2.9.20 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions%2F2.9.20>`__

- Для титула покупателя ``UniversalCorrectionDocumentBuyerTitle`` добавлены методы ``UseSignerDetails`` и ``UseSignerReference``, с помощью которых можно задать объекту значения полей ``SignerDetails`` и ``SignerReference`` соответственно.


01.09.2021
----------
**SDK**: `C# 2.9.19 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions%2F2.9.19>`__

- Добавлена новая версия метода :doc:`/V7/GetNewEvents <http/GetNewEvents>` для получения ленты событий по ящику.
- Для методов :doc:`/V7/GetNewEvents <http/GetNewEvents>` и :doc:`http/GetDocflowEvents_V3` добавлены новые условия фильтрации по критериям:

 - подразделение,
 - тип документа,
 - тип сообщения (письмо, черновик, шаблон),
 - контрагент,
 - направление документооборота (входящий, исходящий, внутренний),
 - время возникновения события.


19.07.2021
----------
**SDK**: `C++ 1.92.6 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/versions%2F1.92.6>`__

- Добавлен метод :doc:`http/GetMyCertificates`, который позволяет получить информацию о сертификатах сотрудника.


29.06.2021
----------
**SDK**: `C# 2.9.15 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions%2F2.9.15>`__

- Добавлены функции документов ``ucd736_05_01_02`` и ``utd820_05_01_02_hyphen`` по приказам №736 и №820.  


25.06.2021
----------
**SDK**: `C# 2.9.14 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions%2F2.9.14>`__ | `Java 3.9.7 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions%2F3.9.7>`__ | `C++ 1.92.4 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/versions%2F1.92.4>`__

- Добавленое поле :doc:`../proto/ConfirmationDocflow` в структуру :doc:`../proto/AmendmentRequestDocflow`.


20.05.2021
----------
**SDK**: `C# 2.9.13 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions%2F2.9.13>`__

- Добавлены структуры для поддержки документов в формате приказа №736 и примеры их использования.


04.05.2021
----------
**SDK**: `C# 2.9.12 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions%2F2.9.12>`__ | `Java 3.9.6 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions%2F3.9.6>`__ | `C++ 1.92.3 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/versions%2F1.92.3>`__

- Добавлен текстовый статус документа :doc:`../proto/DocflowStatusV3` в структуры :doc:`../proto/Document` и :doc:`../proto/DocflowV3`.


23.03.2021
----------
**SDK**: `C# 2.9.9 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions%2F2.9.9>`__ | `Java 3.9.4 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions%2F3.9.4>`__ | `C++ 1.92.2 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/versions%2F1.92.2>`__

- Добавлен признак возможности использовать шаблон больше одного раза.


17.03.2021
----------
**SDK**: `C# 2.9.8 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions%2F2.9.8>`__ | `Java 3.9.3 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions%2F3.9.3>`__ | `C++ 1.92.1 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/versions%2F1.92.1>`__

- В структуре :doc:`../proto/Document` добавлена информация о промежуточном получателе: ``ProxyBoxId`` и ``ProxyDepartmentId``.


17.02.2021
----------
**SDK**: `C# 2.9.5 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions%2F2.9.5>`__ | `Java 3.9.0 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions%2F3.9.0>`__ | `C++ 1.92.0 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/versions%2F1.92.0>`__

- Метод :doc:`http/GetDocumentTypes` заменен второй версией.


10.12.2020
----------
**SDK**: `C# 2.9.0 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions%2F2.9.0>`__ | `Java 3.8.0 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions%2F3.8.0>`__ | `C++ 1.91.0 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/versions%2F1.91.0>`__

- Подготовка клиентов для работы с возможностями частичной приемки.


07.12.2020
----------
**SDK**: `C# 2.8.5 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions%2F2.8.5>`__ | `Java 3.7.4 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions%2F3.7.4>`__ | `C++ 1.90.0 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/versions%2F1.90.0>`__

- В структуры :doc:`../proto/Message` и :doc:`../proto/MessagePatch` добавлена структура ``RevocationRequestInfo``, позволяющая получить информацию о запросе аннулирования.


05.11.2020
----------
**SDK**: `C# 2.8.4 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions%2F2.8.4>`__ | `Java 3.7.3 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions%2F3.7.3>`__ | `C++ 1.89.0 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/versions%2F1.89.0>`__

- В структуре :doc:`../proto/TemplateToPost` добавлены поля ``MessageProxyBoxId`` и ``MessageProxyDepartmentId`` для указания промежуточного получателя документа, который создается из шаблона. ``MessageProxyBoxId`` и ``MessageProxyDepartmentId`` возвращаются в :doc:`../proto/Template` и :doc:`../proto/TemplateToLetterTransformationInfo`.


24.08.2020
----------
**SDK**: `C# 2.7.0 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions%2F2.7.0>`__ | `Java 3.5.0 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions%2F3.5.0>`__ | `C++ 1.86.0 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/versions%2F1.86.0>`__

- В структуре :doc:`../proto/TemplateDocumentAttachment` добавлено поле ``CustomData``.


27.07.2020
----------
**SDK**: `C# 2.6.0 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions%2F2.6.0>`__ | `Java 3.4.0 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions%2F3.4.0>`__ | `C++ 1.85.0 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/versions%2F1.85.0>`__

- В метод :doc:`http/GetOrganizationsByInnList` добавлена инфомация о приглашении контрагента.


14.07.2020
----------
**SDK**: `C# 2.5.0 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions%2F2.5.0>`__ | `Java 3.3.0 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions%2F3.3.0>`__ | `C++ 1.84.0 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/versions%2F1.84.0>`__

- В метод :doc:`http/DssSign` добавлена поддержка подписания сертификатами МЭП.


30.06.2020
----------
**SDK**: `C# 2.3.0 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions%2F2.3.0>`__

- Структура ``DocflowV3`` добавлена в COM API.


24.01.2020
----------
**SDK**: `Java 3.2.1 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions%2F3.2.1>`__

- Удален устаревший код. Убрана обратная совместимость с версией 2.*.*.


20.05.2020
----------
**SDK**: `C# 2.2.0 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions%2F2.2.0>`__ | `Java 3.2.0 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions%2F3.2.0>`__ | `C++ 1.83.0 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/versions%2F1.83.0>`__

- Добавлено поле ``SupportsAmendmentRequest`` в ответ метода :doc:`http/GetDocumentTypes`.
- Добавлены значения в структуры :doc:`http/utd/ExtendedSignerDetailsV2` и :doc:`proto/DocumentTitleType` для поддержки версий формата приказа №423.
- Добавлены значения ``SignerPowers`` и ``SignerStatus`` в структуры :doc:`proto/utd/ExtendedSigner` и :doc:`proto/utd/ExtendedSignerDetailsToPost`.


24.01.2020
----------
**SDK**: `C# 2.0.0 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions%2F2.0.0>`__

- Добавлена поддержка .NET Standard.


26.12.2019
----------
**SDK**: `Java 3.0.0 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions%2F3.0.0>`__

- Выполнен глобальный рефакторинг Java SDK, в котором переработано внутреннее устройство библиотеки, обновлены зависимости и произведены некоторые breaking changes.
- Добавлена поддержка подписания по ГОСТ 2012 в ``CertificateHelper``. Библиотека сама определяет ГОСТ сертификата, и подписывает соответствующим алгоритмом.
- Выполнено изменение контракта ошибок: сейчас любая ошибка оборачивается в тип ``DiadocSdkException``.
- Добавлены доменные клиенты, обратиться к которым можно через корневой объект ``DiadocApi``. Методы перемещены по соответствующим доменным клиентам, а в старых методах сделаны перевызовы. Все старые методы помечены ``Deprecated``, и будут удалены в ближайшее время.
- Breaking changes:

 - тип ``GeneratedFile`` перемещен в пакет ``Diadoc.Api.httpClient``;
 - тип ``DiadocErrorException`` переименоват в ``DiadocException``;
 - тип ``DocumentsFilter`` перемещен в пакет ``Diadoc.Api.document``. Изменен его интерфейс: удалены публичные поля, вместо них добавлены fluent setters;
 - в классе ``CertificateHelper`` методы переименованы на camelCase нотацию.


24.12.2019
----------
**SDK**: `C# 1.87.0 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions%2F1.87.0>`__ | `Java 2.21.0 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions%2F2.21.0>`__ | `C++ 1.82.0 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/versions%2F1.82.0>`__

- Добавлен метод :doc:`http/PostTemplatePatch`, который позволяет отправлять дополнения к шаблонам документов.
- Добавлена возможность с помощью этого метода и структуры :ref:`TemplateRefusalAttachment <template-refusal-attachment>` выполнить отзыв или отклонение шаблона.
- В структуры :doc:`proto/Entity message` и :ref:`DocumentTemplateInfo <document-template-info>` добавлена информация об отзыве и отклонении шаблона.


13.12.2019
----------
**SDK**: `C# 1.86.0 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions%2F1.86.0>`__ | `Java 2.20.0 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions%2F2.20.0>`__ | `C++ 1.81.0 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/versions%2F1.81.0>`__

- Добавлен метод :doc:`http/DetectDocumentTitles`, который позволяет определить возможные типы документа у конкретного файла.


12.12.2019
----------
**SDK**: `C# 1.85.3 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions%2F1.85.3>`__ | `Java 2.19.1 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions%2F2.19.1>`__

- Следующие методы теперь могут возвращать неточное количество событий ``TotalCount``:

 - :doc:`http/GetNewEvents`
 - :doc:`http/GetDocflowEvents`
 - :doc:`http/GetDocflowEvents_V3`
 - :doc:`http/GetForwardedDocumentEvents`


25.11.2019
----------
**SDK**: `C# 1.85.0 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions%2F1.85.0>`__

- Добавлен метод :doc:`http/GetMyCertificates`, который позволяет получить информацию о сертификатах сотрудника.


30.09.2019
----------
**SDK**: `C# 1.84.0 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions%2F1.84.0>`__ | `Java 2.19.0 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions%2F2.19.0>`__ | `C++ 1.80.0 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/versions%2F1.80.0>`__

- Добавлен метод :doc:`http/GenerateReceiptXml`, который генерирует извещение о получении на любую сущность в документообороте, для которой оно требуется.
- Для обратной совместимости старые URL-адреса ``GenerateDocumentReceiptXml`` и ``GenerateInvoiceDocumentReceiptXml`` расширены и поддерживают весь функционал нового метода.


18.09.2019
----------
**SDK**: `C# 1.83.0 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions%2F1.83.0>`__ | `Java 2.18.0 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions%2F2.18.0>`__ | `C++ 1.79.0 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/versions%2F1.79.0>`__

- Добавлены методы :doc:`http/DssSign` и :doc:`http/DssSignResult` для :doc:`подписания DSS-сертификатом <API_Dss>`.


17.09.2019
----------
**SDK**: `C# 1.82.1 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions%2F1.82.1>`__

- Добавлена новая версия ``utd820_05_01_01_hyphen`` для всех типов документов, поддерживающих формат приказа №820: счета-фактуры и их исправления, акты, накладные, УПД, иУПД. Версия полностью совместима с ``utd820_05_01_01``. Отличается только генерация и парсинг. Теперь при генерации необходимо явно задать следующие атрибуты и при парсинге учитывать наличие этих атрибутов в ``UserDataXML``:

 - *ДефНомИспрСчФ*
 - *ДефДатаИспрСчФ*
 - *ДефОКЕИ_Тов*
 - *ДефСтТовУчНал*
 - *ДефСтТовУчНалВсего*
 - *ДефКодПроисх*
 - *ДефИННЮЛ*
 - *ДефИННФЛ*
 - *ДефНДС*.
 
 Также можно явно указывать ФНС-идентификаторы отправителя (*ИдОтпр*) и получателя (*ИдПол*). Может быть полезно в случаях, когда в документе указано несколько продавцов (элемент xml *СвПрод*) или покупателей (*СвПокуп*), и нужно явно определить, кто из них является участником документооборота.
 Подробные отличия можно посмотреть в XSD-схеме, доступной в поле *UserDataXSD* ответа метода :doc:`http/GetDocumentTypes`.
 
- Для C# SDK добавлена кодогенерация новой XSD, доступной по `ссылке <https://github.com/diadoc/diadocsdk-csharp/blob/master/src/DataXml/Utd820/Hyphens/ON_NSCHFDOPPR_UserContract_820_05_01_01_Hyphen.cs>`__.


17.09.2019
----------
**SDK**: `C# 1.82.0 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions%2F1.82.0>`__ | `Java 2.17.0 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions%2F2.17.0>`__ | `C++ 1.78.2 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/versions%2F1.78.2>`__ 

- Добавлена новая версия метода :doc:`http/Authenticate` с универсальным контрактом, в котором все данные для аутентификации передаются в теле POST запроса.


06.09.2019
----------
**SDK**: `C# 1.81.0 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions%2F1.81.0>`__ | `Java 2.16.1 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions%2F2.16.0>`__ | `C++ 1.78.2 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/versions%2F1.78.0>`__

- В возвращаемое значение метода :doc:`http/AcquireCounteragentResult` добавлено поле ``InvitationDocumentId``.
- В структуре :doc:`proto/Counteragent` добавлено поле ``InvitationDocumentId``.


27.08.2019
----------
**SDK**: `Java 2.16.0 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions%2F2.16.0>`__ | `C++ 1.78.0 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/versions%2F1.78.0>`__

- В Java и C++ SDK добавлен метод :doc:`http/GenerateTitleXml`, позволяющий сгенерировать любой титул любого типа документа.
- В Java и C++ SDK в структуре :doc:`DocumentTitle <proto/DocumentTypeDescription>` добавлено поле ``Index`` для обозначения порядкового номера титула в документе.


16.08.2019
----------
**SDK**: `C# 1.80.0 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions%2F1.80.0>`__ | `Java 2.15.0 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions%2F2.15.0>`__ | `C++ 1.77.0 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/versions%2F1.77.0>`__

- Добавлен метод :doc:`http/GetLastEvent`, возвращающий последнее событие в ящике.


15.08.2019
----------
**SDK**: `C# 1.79.0 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions%2F1.79.0>`__ 

- В C# SDK добавлен метод :doc:`http/GenerateTitleXml`, позволяющий сгенерировать любой титул любого типа документа.
- В C# SDK в структуре :doc:`DocumentTitle <proto/DocumentTypeDescription>` добавлено поле ``Index`` для обозначения порядкового номера титула в документе.


05.08.2019
----------
**SDK**: `C# 1.78.0 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions%2F1.78.0>`__ | `Java 2.14.0 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions%2F2.14.0>`__ | `C++ 1.76.0 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/versions%2F1.76.0>`__

- В метод :doc:`http/utd/GenerateUniversalTransferDocumentXmlForSeller` добавлен опциональный параметр ``documentVersion``.


14.07.2019
----------
**SDK**: `C# 1.77.0 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions%2F1.77.0>`__ | `Java 2.13.0 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions%2F2.13.0>`__ | `C++ 1.75.0 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/versions%2F1.75.0>`__

- Добавлен метод :doc:`http/DetectCustomPrintForms`, возвращающий информацию о наличии у документа нестандратной печатной формы.
- Свойство ``HasCustomPrintForms`` структуры :doc:`proto/Document` объявлено устаревшим и больше не заполняется (всегда возвращается ``false``).


09.07.2019
----------
**SDK**: `C# 1.76.0 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions%2F1.76.0>`__ | `Java 2.12.0 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions%2F2.12.0>`__ | `C++ 1.74.0 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/versions%2F1.74.0>`__

- Добавлен метод :doc:`http/GetMyEmployee`, возвращающий информацию о текущем сотруднике организации.
- Метод :doc:`http/GetMyPermissions` объявлен устаревшим.
- Добавлена возможность управлять правом сотрудника удалять документы и черновики и восстанавливать документы с помощью метода :doc:`proto/EmployeePermissions`. В структуре :doc:`proto/OrganizationUserPermissions` добавлен флаг ``CanDeleteRestoreDocuments``.


09.07.2019
----------
**SDK**: `C# 1.75.0 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions%2F1.75.0>`__ | `Java 2.11.1 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions%2F2.11.1>`__ | `C++ 1.73.0 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/versions%2F1.73.0>`__

- Поле ``TransferDocDetails`` в структуре :doc:`EventContent <proto/utd/UniversalCorrectionDocumentSellerTitleInfo>`, соответствующее атрибуту *ПередатДокум* в УКД, стало необязательным.


05.07.2019
----------
**SDK**: `C# 1.74.0 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/1.74>`__ | `Java 2.10.0 <https://github.com/diadoc/diadocsdk-java/releases/tag/2.10.0>`__ | `C++ 1.72.0 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/1.72.0>`__

- Добавлена возможность отправлять шаблоны из/в подразделение методом :doc:`http/PostTemplate`.
- Добавлена возможность перемещать шаблоны между подразделениями методом :doc:`http/MoveDocuments`.


11.06.2019
----------
**SDK**: `C# 1.73.0 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions%2F1.73.0>`__ | `Java 2.9.0 <https://github.com/diadoc/diadocsdk-java/releases/tag/2.9.0>`__ | `C++ 1.71.0 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/1.71.0>`__

- Обновлена версия методов :doc:`http/GetNewEvents` и :doc:`http/GetMessage`. Новая версия возвращает события по шаблонам :doc:`proto/Message` и :doc:`proto/MessagePatch`.
- В метод :doc:`http/GetDocflowEvents_V3` добавлена информация о шаблонах.


27.05.2019
----------
**SDK**: `C# 1.72.0 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions/1.72.0>`__ | `Java 2.8.0 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions/2.8.0>`__ | `C++ 1.70.0 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/versions/1.70.0>`__

- Добавлена поддержка формата `приказа №820 <https://normativ.kontur.ru/document?moduleId=1&documentId=328588>`__:

 - через метод :doc:`http/GetDocumentTypes` можно найти версии с идентификатором ``utd820_05_01_01`` для всех типов документов, поддерживающих новый формат: счета-фактуры, акты, накладные, УПД, иУПД.
 - для генерации и парсинга документов новой версии доступны только обобщенные методы:
 
  - :doc:`http/GenerateSenderTitleXml`,
  - :doc:`http/GenerateRecipientTitleXml`,
  - :doc:`http/ParseTitleXml`.
  
- В структуры :doc:`proto/utd/ExtendedSigner` и :doc:`proto/DocumentTitleType` добавлены значения в для поддержки версий формата приказа №820.


16.05.2019
----------
**SDK**: `C# 1.71.0 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions/1.71.0>`__ | `Java 2.7.0 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions/2.7.0>`__ | `C++ 1.69.0 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/versions/1.69.0>`__

- Добавлен метод :doc:`http/Organizations/GetOrganizationFeatures` для возвращения статуса блокировки ящика и прочих фич ящика.


14.05.2019
----------
**SDK**: `C# 1.70.0 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions/1.70.0>`__ | `Java 2.6.0 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions/2.6.0>`__ | `C++ 1.68.0 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/versions/1.68.0>`__

- Добавлен метод :doc:`http/ParseTitleXml` для парсинга документа любой версии.


07.05.2019
----------
**SDK**: `C# 1.69.0 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions/1.69.0>`__ | `Java 2.5.0 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions/2.5.0>`__ | `C++ 1.67.0 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/versions/1.67.0>`__

- Добавлены методы :doc:`http/Register` и :doc:`http/RegisterConfirm` для регистрации организации и сотрудника по сертификату.


24.04.2019
----------
**SDK**: `C# 1.68.0 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions/1.68.0>`__ | `Java 2.4.0 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions/2.4.0>`__

- В структуре :doc:`proto/DocflowV3`:

 - удалена структура ``ProxyResponseDocflow``;
 - изменена структура ``RecipientResponseDocflow``:
 
  - структура переименована в :doc:`proto/ParticipantResponseDocflow`;
  - поле ``RecipientTitle`` переименовано в ``Title``;
  - Поле ``RecipientResponseStatus`` переименовано ``ResponseStatus``;
  
 - удалено поле ``ProxyResponse = 3``, вместо него добавлено поле ``ProxyResponse = 11``, структура которого соответствует :doc:`proto/ParticipantResponseDocflow`.


23.04.2019
----------
**SDK**: `C# 1.67.0 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions/1.67.0>`__ | `Java 2.3.0 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions/2.3.0>`__

- В структуре :doc:`proto/DocflowV3` добавлены свойства, содержащие текстовые выдержки соответствующих документов.
- В структуре :doc:`proto/SignatureRejectionDocflow` добавлено свойство ``PlainText``, которое содержит текст сообщения об отказе в подписи.
- В структуре :doc:`proto/AmendmentRequestDocflow` добавлено свойство ``PlainText``, которое содержит текст запроса уточнения.
- В структуре :doc:`RevocationRequestDocflow <proto/RevocationDocflowV3>` добавлено свойство ``PlainText``, которое содержит текст запроса аннулирования.


09.03.2019
----------
**SDK**: `C# 1.65.0 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions/1.65.0>`__ | `Java 2.1.0 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions/2.1.0>`__ | `C++ 1.65.0 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/versions/1.65.0>`__

- В структуре :doc:`ResolutionRequestType <proto/ResolutionRequest>` добавлен тип согласования ``Custom``.
- В структуре :doc:`ResolutionRequestInfo <proto/ResolutionRequest>` добавлено свойство ``Actions``, в котором перечислены доступные действия для запроса согласования.
- В структуре :doc:`ResolutionStatusType <proto/ResolutionStatus>` добавлен тип запроса согласования ``ActionsRequested``, который соответствует типу ``Custom``.
- В структуре :doc:`ResolutionStatus <proto/ResolutionDocflowV3>` добавлено свойство ``ActionsRequested``.
- В структуре :doc:`ResolutionRequestV3 <proto/ResolutionEntitiesV3>` добавлено свойство ``Actions``, в котором перечислены доступные действия для запроса согласования.


30.01.2019
----------
**SDK**: `Java 2.0.0 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions/2.0.0>`__

- Обновлен JDK до версии 10.x
- Обновлен КриптоПро JCP до версии 2.0


15.01.2019
----------
**SDK**: `C# 1.64.0 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions/1.64.0>`__ | `Java 1.64.0 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions/1.64.0>`__ | `C++ 1.64.0 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/versions/1.64.0>`__

- Добавлен метод :doc:`http/Departments/GetDepartment` для получения информацию о подразделении организации.
- Добавлен метод :doc:`http/Departments/GetDepartments` для получения списка подразделений организации.
- Добавлен метод :doc:`http/Departments/CreateDepartment` для создания подразделения организации.
- Добавлен метод :doc:`http/Departments/UpdateDepartment` для обновления подразделения организации.
- Добавлен метод :doc:`http/Departments/DeleteDepartment` для удаления подразделения организации.


26.12.2018
----------
**SDK**: `C# 1.63.0 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions/1.63.0>`__ | `Java 1.63.0 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions/1.63.0>`__ | `C++ 1.63.0 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/versions/1.63.0>`__

- Добавлена возможность блокировки сотрудников в организации. Для этого расширены структуры:

 - :doc:`proto/EmployeePermissions`,
 - :doc:`EmployeePermissionsPatch <proto/EmployeeToUpdate>`,
 - :doc:`proto/OrganizationUserPermissions`.


24.12.2018
----------
**SDK**: `C# 1.62.1 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions/1.62.1>`__ | `Java 1.62.1 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions/1.62.1>`__ | `C++ 1.62.1 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/versions/1.62.1>`__

- Следующие методы генерации и парсинга документов получили поддержку ставки 20%:

 - :doc:`http/GenerateInvoiceXml` — для генерации счетов-фактур,
 - :doc:`http/GenerateTorg12XmlForSeller` — для генерации документов в формате приказа 551,
 - :doc:`http/GenerateAcceptanceCertificateXmlForSeller` — для генерации документов в формате приказа 552,
 - :doc:`http/utd/GenerateUniversalTransferDocumentXmlForSeller` — для генерации документов в форматах УПД и УКД,
 - :doc:`http/ParseInvoiceXml` — для парсинга счетов-фактур,
 - :doc:`http/ParseTorg12SellerTitleXml` — для парсинга документов в формате приказа 551,
 - :doc:`http/ParseAcceptanceCertificateSellerTitleXml` — для парсинга документов в формате приказа 552,
 - :doc:`http/utd/ParseUniversalTransferDocumentSellerTitleXml` — для парсинга документов в формате УПД,
 - :doc:`http/utd/ParseUniversalCorrectionDocumentSellerTitleXml` — для парсинга документов в формате УКД.


14.12.2018
----------
**SDK**: `C# 1.62.0 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions/1.62.0>`__ | `Java 1.62.0 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions/1.62.0>`__ | `C++ 1.62.0 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/versions/1.62.0>`__

- Добавлено поле ``Version`` в следующие структуры:

 - :doc:`proto/DocumentInfo`
 - :doc:`proto/Document`
 - :doc:`Entity <proto/Entity message>`


05.12.2018
----------

- Добавлен метод :doc:`http/GetEmployees` для получения списка сотрудников организации.


28.11.2018
----------
**SDK**: `C# 1.60.1 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions/1.60.1>`__ | `Java 1.60.1 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions/1.60.1>`__ | `C++ 1.60.1 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/versions/1.60.1>`__

- В структуре :doc:`proto/DocflowV3` добавлена информация о согласовании документа.


30.10.2018
----------
**SDK**: `C# 1.59.0 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions/1.59.0>`__ | `Java 1.59.0 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions/1.59.0>`__ | `C++ 1.59.0 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/versions/1.59.0>`__

- Добавлена возможность работы с извещением о получении на титул получателя:

 - обновлены настройки документооборота :doc:`proto/DocumentWorkflow` для всех типов документа, добавлена новая настройка;
 - в структуре :doc:`proto/MessagePatchToPost` следующие поля сменили сообщение протобуфера с ``ReceiptAttachment`` на ``RecipientTitleAttachment``:
 
  - ``RecipientTitles``,
  - ``XmlTorg12BuyerTitles``,
  - ``XmlAcceptanceCertificateBuyerTitles``,
  - ``UniversalTransferDocumentBuyerTitles``;
  
 - в структуре :doc:`proto/Document` добавлено поле ``SenderReceiptMetadata``;
 - в структуре :doc:`proto/DocflowV3` добавлено поле ``SenderReceipt``.


22.10.2018
----------
**SDK**: `C# 1.58.0 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions/1.58.0>`__ | `Java 1.58.0 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions/1.58.0>`__ | `C++ 1.58.0 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/versions/1.58.0>`__

- Добавлен метод :doc:`http/DeleteEmployee` для удаления сотрудника.


22.10.2018
----------
**SDK**: `C# 1.57.0 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions/1.57.0>`__ | `Java 1.57.0 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions/1.57.0>`__ | `C++ 1.57.0 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/versions/1.57.0>`__

- Добавлен метод :doc:`http/UpdateEmployee` для редактирования сотрудника.


16.10.2018
----------
**SDK**: `C# 1.56.0 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions/1.56.0>`__ | `Java 1.56.0 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions/1.56.0>`__ | `C++ 1.56.0 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/versions/1.56.0>`__

- В структуре :doc:`DocumentTitle <proto/DocumentTypeDescription>` добавлена информация о типе подписанта ``SignerInfo``, необходимого для подписания титула.


04.10.2018
----------
**SDK**: `C# 1.55.7 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions/1.55.7>`__ | `Java 1.55.7 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions/1.55.7>`__ | `C++ 1.55.7 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/versions/1.55.7>`__

- Добавлен метод :doc:`http/UpdateMyUser` для редактирования данных пользователя.


02.10.2018
----------
**SDK**: `C# 1.55.6 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions/1.55.6>`__ | `Java 1.55.6 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions/1.55.6>`__ | `C++ 1.55.6 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/versions/1.55.6>`__

- Добавлен механизм для отправки предопределенного титула получателя. Подробности на странице :doc:`/howto/example_predefined_recipient_title`.


17.09.2018
----------
**SDK**: `C# 1.54.6 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions/1.54.6>`__ | `Java 1.54.6 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions/1.54.6>`__ | `C++ 1.54.6 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/versions/1.54.6>`__

- Добавлен метод :doc:`http/CreateEmployee` для создания сотрудника.


07.09.2018
----------
**SDK**: `C# 1.54.4 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions/1.54.4>`__ | `Java 1.54.4 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions/1.54.4>`__ | `C++ 1.54.4 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/versions/1.54.4>`__

- В структуре :doc:`proto/DocumentList` добавлено поле ``HasMoreResults``. Если количество документов превышает 1000, значение ``TotalCount`` всегда будет возвращаться равным 1000, а признак ``HasMoreResults = true``.


31.08.2018
----------
**SDK**: `C# 1.54.1 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions/1.54.1>`__ | `Java 1.54.1 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions/1.54.1>`__ | `C++ 1.54.1 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/versions/1.54.1>`__

- Добавлена возможность управлять правом сотрудника видеть списки контрагентов и работать с ними с помощью метода :doc:`proto/EmployeePermissions`.
- В структуре :doc:`proto/OrganizationUserPermissions` добавлено поле ``CanManageCounteragents``.


29.08.2018
----------
**SDK**: `C# 1.54.0 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions/1.54.0>`__ | `Java 1.54.0 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions/1.54.0>`__ | `C++ 1.54.0 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/versions/1.54.0>`__

- Добавлен метод получения подписок сотрудника на почтовые уведомления :doc:`http/GetSubscriptions` и метод для их редактирования :doc:`http/UpdateSubscriptions`.


20.08.2018
----------
**SDK**: `C# 1.53.0 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions/1.53.0>`__ | `Java 1.53.0 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions/1.53.0>`__ | `C++ 1.53.0 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/versions/1.53.0>`__

- Добавлен обобщенный метод генерации титула отправителя :doc:`http/GenerateSenderTitleXml`.


08.08.2018
----------
**SDK**: `C# 1.52.4 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions/1.52.4>`__

- В C# SDK добавлены экспериментальные версии методов Docflow API:

 - :doc:`http/GetDocflows_V3`
 - :doc:`http/GetDocflowEvents_V3`
 - :doc:`http/GetDocflowsByPacketId_V3`
 - :doc:`http/SearchDocflows_V3`


07.08.2018
----------
**SDK**: `C# 1.52.3 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions/1.52.3>`__ | `Java 1.52.3 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions/1.52.3>`__ | `C++ 1.52.3 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/versions/1.52.3>`__

- Добавлен метод получения сотрудника :doc:`http/GetEmployee` и новая версия метода :doc:`http/GetMyUser`.


06.08.2018
----------
**SDK**: `C# 1.52.1 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions/1.52.1>`__ | `Java 1.52.1 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions/1.52.1>`__ | `C++ 1.52.1 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/versions/1.52.1>`__

- В структуре :doc:`proto/Organization` добавлено поле ``HasCertificateToSign``.


19.07.2018
----------
**SDK**: `C# 1.52.0 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions/1.52.0>`__ | `Java 1.52.0 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions/1.52.0>`__ | `C++ 1.52.0 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/versions/1.52.0>`__

- Добавлены режимы блокировки сообщений с шаблонами :doc:`proto/LockMode`. Режим можно указать при отправке шаблонов через :doc:`TemplateToPost <proto/TemplateToPost>`.
- Добавлена поддержка удаления и восстановления шаблонов через имеющиеся методы :doc:`http/Delete` и :doc:`http/Restore`.


04.07.2018
----------
**SDK**: `C# 1.51.9 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions/1.51.9>`__ | `Java 1.51.9 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions/1.51.9>`__ | `C++ 1.51.9 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/versions/1.51.9>`__

- В структуре :doc:`proto/Docflow` добавлено поле :doc:`proto/Docflow_RoamingNotification`, содержащее данные о доставке документа в роуминг.


25.06.2018
----------
**SDK**: `C# 1.51.8 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions/1.51.8>`__ | `Java 1.51.8 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions/1.51.8>`__ | `C++ 1.51.8 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/versions/1.51.8>`__

- Добавлены режимы блокировки сообщений :doc:`proto/LockMode`.


14.06.2018
----------
**SDK**: `C# 1.51.7 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions/1.51.7>`__ | `Java 1.51.7 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions/1.51.7>`__ | `C++ 1.51.7 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/versions/1.51.7>`__

- В структуре :doc:`proto/Document` добавлено поле ``EditingSettingId``, содержащее идентификатор настройки документа, если он был создан из шаблона с возможностью редактирования полей.
- В структуре :doc:`proto/OrganizationUserPermissions` добавлено поле ``CanCreateDocuments``, указывающее, может ли пользователь создавать документы и работать с черновиками.


22.05.2018
----------
**SDK**: `C# 1.51.6 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions/1.51.6>`__

- Добавлен обобщенный метод генерации титула получателя :doc:`http/GenerateRecipientTitleXml`.
- Расширена структура :doc:`DocumentTitle <proto/DocumentTypeDescription>`: добавлено поле ``UserDataXsdUrl``, позволяющее узнать, по какой ссылке возможно загрузить XSD-схему контракта для генерации титула с помощью обобщенного метода генерации :doc:`http/GenerateRecipientTitleXml`.


23.04.2018
----------
**SDK**: `C# 1.51.3 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions/1.51.3>`__ | `Java 1.51.3 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions/1.51.3>`__ | `C++ 1.51.3 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/versions/1.51.3>`__

- Расширена структура :doc:`proto/Document`: добавлено свойство :doc:`proto/Origin`, позволяющее узнать, из какого черновика или шаблона был создан документ.


16.04.2018
----------
**SDK**: `C# 1.51.2 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions/1.51.2>`__

- Расширена структура :doc:`proto/MessagePatchToPost`: добавлен необязательный список операций ``EditingPatches`` для редактирования контента документа.


12.04.2018
----------
**SDK**: `C# 1.51.1 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions/1.51.1>`__ | `Java 1.51.1 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions/1.51.1>`__ | `C++ 1.51.1 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/versions/1.51.1>`__

- Расширена структура :doc:`proto/TemplateDocumentAttachment`:

 - добавлен необязательный признак ``NeedRecipientSignature``, обозначающий запрос подписи получателя под отправляемым документом, созданным из шаблона;
 - добавлен необязательный идентификатор настройки редактирования содержимого документа :doc:`EditingSettingId <proto/TemplateDocumentAttachment>`.


29.03.2018
----------
**SDK**: `C# 1.51 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions/1.51>`__ | `Java 1.51 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions/1.51>`__ | `C++ 1.51 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/versions/1.51>`__

- Добавлены метки :doc:`proto/Labels`.
- Свойство ``Labels`` добавлено в следующие структуры:

 - :doc:`Entity <proto/Entity message>`
 - :doc:`ReceiptAttachment <proto/MessagePatchToPost>`
 - :doc:`CorrectionRequestAttachment <proto/MessagePatchToPost>`
 - :doc:`DocumentSignature <proto/MessagePatchToPost>`
 - :doc:`SignatureVerification <proto/MessagePatchToPost>`
 - :doc:`ResolutionAttachment <proto/Resolution>`
 - :doc:`ResolutionRequestAttachment <proto/ResolutionRequest>`
 - :doc:`ResolutionRouteAssignment <proto/MessagePatchToPost>`
 - :doc:`ResolutionRequestCancellationAttachment <proto/ResolutionRequest>`
 - :doc:`ResolutionRequestDenialAttachment <proto/ResolutionRequestDenial>`
 - :doc:`RequestedSignatureRejection <proto/MessagePatchToPost>`
 - :doc:`RevocationRequestAttachment <proto/MessagePatchToPost>`
 - :doc:`XmlSignatureRejectionAttachment <proto/MessagePatchToPost>`


26.02.2018
----------
**SDK**: `C# 1.50 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions/1.50>`__ | `Java 1.50 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions/1.50>`__ | `C++ 1.50 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/versions/1.50>`__

- Расширена структура контракта :doc:`proto/Document`: добавлены свойства для универсальной работы с документом.
- Следующие свойства считаются **устаревшими** и **не рекомендованы** к использованию, — в будущем они будут удалены:

 - ``NonformalizedDocumentMetadata``
 - ``InvoiceMetadata``
 - ``InvoiceRevisionMetadata``
 - ``InvoiceCorrectionMetadata``
 - ``InvoiceCorrectionRevisionMetadata``
 - ``TrustConnectionRequestMetadata``
 - ``Torg12Metadata``
 - ``AcceptanceCertificateMetadata``
 - ``ProformaInvoiceMetadata``
 - ``XmlTorg12Metadata``
 - ``XmlAcceptanceCertificateMetadata``
 - ``PriceListMetadata``
 - ``PriceListAgreementMetadata``
 - ``CertificateRegistryMetadata``
 - ``ReconciliationActMetadata``
 - ``ContractMetadata``
 - ``Torg13Metadata``
 - ``SupplementaryAgreementMetadata``
 - ``ServiceDetailsMetadata``
 - ``UniversalTransferDocumentMetadata``
 - ``UniversalTransferDocumentRevisionMetadata``
 - ``UniversalCorrectionDocumentMetadata``
 - ``UniversalCorrectionDocumentRevisionMetadata``


08.02.2018
----------
**SDK**: `C# 1.49.2 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions/1.49.2>`__ | `Java 1.49.2 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions/1.49.2>`__ | `C++ 1.49.2 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/versions/1.49.2>`__

- Расширена структура :doc:`proto/PrepareDocumentsToSignRequest` метода :doc:`http/PrepareDocumentsToSign`: добавлена структура ``ContentToPatch`` для патчинга содержимого документов.
- Добавлен метод для создания сообщения с документами на основе шаблона :doc:`http/TransformTemplateToMessage`.
- Добавлена универсальная структура в ``MessagePatchToPost.RecipientTitles`` для отправки второго титула любого типа документов. Рекомендуем использовать это поле вместо ``XmlTorg12BuyerTitles``, ``XmlAcceptanceCertificateBuyerTitles``, ``UniversalTransferDocumentBuyerTitles`` и др.


09.01.2018
----------
**SDK**: `C# 1.49.1 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions/1.49.1>`__ | `Java 1.49.1 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions/1.49.1>`__ | `C++ 1.49.1 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/versions/1.49.1>`__

- Добавлен параметр ``count`` для метода :doc:`http/GetDocuments`.


21.12.2017
----------
**SDK**: `C# 1.49 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions/1.49>`__ | `Java 1.49 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions/1.49>`__ | `C++ 1.49 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/versions/1.49>`__

- Добавлены методы для работы с шаблонами документов:

 - :doc:`http/PostTemplate` — для отправки шаблона документов,
 - :doc:`http/GetTemplate` — для получения отправленного шаблона.
 
- В структуре ``Organization`` добавлено поле ``IsForeign``, отражающее статус иностранности организации.


25.10.2017
----------
**SDK**: `C# 1.48 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions/1.48>`__

- Добавлен метод :doc:`http/GetDocumentTypes`, возвращающий описание типов документов, доступных в ящике.
- В структуре :doc:`proto/MessageToPost`, которую принимает метод :doc:`/V3/PostMessage <http/PostMessage>`, изменилось поле ``CustomDocumentAttachments``. Теперь оно называется :doc:`proto/DocumentAttachment` и может использоваться для отправки документов любых типов.


19.10.2017
----------

- Добавлено ограничение на количество документов в структуре :doc:`proto/MessageToPost`, которую можно отправить через метод :doc:`http/PostMessage`. Текущее максимальное количество документов в сообщении — 30.


18.09.2017
----------
**SDK**: `C# 1.47.1 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions/1.47.1>`__ | `Java 1.47.1 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions/1.47.1>`__ | `C++ 1.47.1 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/versions/1.47.1>`__

- В структуре :doc:`../proto/User`, которая возвращается методом :doc:`http/GetMyUser`, изменилась структура ``CertificateInfo``. В нее добавлены поля:

 - ``OrganizationName`` — наименование организации, на которую выдан сертификат,
 - ``Inn`` — ИНН организации, на которую выдан сертификат.


06.09.2017
----------
**SDK**: `C# 1.47 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions/1.47>`__ | `Java 1.47 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions/1.47>`__ | `C++ 1.47 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/versions/1.47>`__

- Добавлена новая версия метода :doc:`/V4/GetMessage <http/GetMessage>`. Основное отличие версии *V4* от версии *V3* в том, что новая версия метода имеет дополнительную опцию ``injectEntityContent``.


31.08.2017
----------

- Добавлена структура :doc:`proto/CancellationInfo`, содержащая информацию об отмене сущности.
- Изменилось поведение метода :doc:`http/GetMessage`: отмененные запросы на согласование возвращаются вместе с соответствующими сущностями отмены. Раньше отмененный запрос на согласование не возвращался, и не было возможности определить, что данный запрос на соглавание был отменен.


30.08.2017
----------
**SDK**: `C# 1.46.1 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions/1.46.1>`__ | `Java 1.46.1 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions/1.46.1>`__ | `C++ 1.46.1 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/versions/1.46.1>`__

- Добавлены структуры :doc:`proto/TovTorgInfo` и :doc:`proto/AcceptanceCertificate552Info` для описания накладных и актов в формате приказов №551/552.


23.08.2017
----------
**SDK**: `C# 1.46 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions/1.46>`__ | `Java 1.46 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions/1.46>`__ | `C++ 1.46 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/versions/1.46>`__

- Добавлена структура :doc:`proto/SignatureInfo`, содержащая информацию о подписи и сертификате.
- Добавлен метод :doc:`http/GetSignatureInfo`, получающий на вход идентификаторы подписи и возвращающий данные в структуре :doc:`proto/SignatureInfo`.
- В структуре :doc:`InvoiceItemAmountsDiff <proto/InvoiceCorrectionInfo>` поле ``Subtotal``, отражающее сумму с учетом налога, теперь является опциональным.
- Добавлена вторая версия метода :doc:`ExtendedSignerDetails <http/utd/ExtendedSignerDetailsV2>`, принимающая на вход структуру :doc:`proto/DocumentTitleType`.


13.07.2017
----------
**SDK**: `C# 1.44.2 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions/1.44.2>`__ | `Java 1.44.2 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions/1.44.2>`__ | `C++ 1.44.2 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/versions/1.44.2>`__

- В структуре :doc:`proto/Organization` добавлено поле ``CertificateOfRegistryInfo``, в котором указана информация о свидетельстве о государственной регистрации.
- В структуре :doc:`proto/DocumentInfo` добавлено поле ``AttachmentVersion``, в котором указана версия документа.


29.06.2017
----------
**SDK**: `C# 1.44.1 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions/1.44.1>`__ | `Java 1.44.1 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions/1.44.1>`__ | `C++ 1.44.1 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/versions/1.44.1>`__

- Добавлен признак «Разрешить посылать зашифрованные документы».
- В структуре :doc:`Box <proto/Organization>` добавлено поле ``EncryptedDocumentsAllowed``, в котором указан признак «Разрешить посылать зашифрованные документы».


06.06.2017
----------
**SDK**: `C# 1.44 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions/1.44>`__ | `Java 1.44 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions/1.44>`__ | `C++ 1.44 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/versions/1.44>`__

- В структуре :doc:`proto/EncryptedXmlDocumentAttachment` добавлено поле ``DocumentName``, в котором указано наименование первичного документа, определенное организацией (*НаимДокОпр*).


02.06.2017
----------
**SDK**: `C# 1.43 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions/1.43>`__ | `Java 1.43 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions/1.43>`__ | `C++ 1.43 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/versions/1.43>`__

- Добавлена дата ликвидации организации.
- В структуре :doc:`proto/Organization` добавлено поле ``LiquidationDate``, в котором указана дата ликвидации организации по данным из ЕГРЮЛ и ЕГРИП.


03.05.2017
----------

- Добавлены подписи промежуточных получателей и их статусы:

 - в структуре :doc:`proto/Document` добавлено поле ``ProxySignatureStatus``, отвечающее за статус подписи промежуточного получателя.
 - в структуре :doc:`proto/Message` в поле ``Entities`` теперь возвращаются сами подписи промежуточного получателя.


11.04.2017
----------
**SDK**: `C# 1.41.3 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions/1.41.3>`__ | `Java 1.41.3 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions/1.41.3>`__ | `C++ 1.41.3 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/versions/1.41.3>`__

- Добавлена возможность определить версию XSD-схемы, в соответствии с которой был отправлен документ: в структурах :doc:`proto/Document` и :doc:`Entity <proto/Entity message>` добавлено поле ``AttachmentVersion``. Значения, возвращаемые в этом поле, показывают версию XSD-схемы. Версия XSD возвращается для документов, сформированных в соответствии с приказами ФНС №155 от 24 марта 2016 и №189 от 13 апреля 2016. В дальнейшем планируется расширение перечня возвращаемых значений.


30.03.2017
----------
**SDK**: `C# 1.41.1 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions/1.41.1>`__ | `Java 1.41.1 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions/1.41.1>`__ | `C++ 1.41.1 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/versions/1.41.1>`__

- Добавлена возможность отправлять неформализованные акты и акты сверки без указания номера документа: в структурах :doc:`proto/ReconciliationActAttachment` и :doc:`proto/AcceptanceCertificateAttachment` поле ``DocumentNumber`` стало необязательным.


27.03.2017
----------
**SDK**: `C# 1.41 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions/1.41>`__ | `Java 1.41 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions/1.41>`__ | `C++ 1.41 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/versions/1.41>`__

- Добавлена возможность снимать документ с маршрута согласования с помощью поля ``ResolutionRouteRemovals`` в структуре :doc:`proto/MessagePatchToPost`.
- Переименования:

 - в документации термин «цепочка согласования» заменен на «маршрут согласования»,
 - в названиях структур и HTTP-методах слово «Chain» заменено на «Route»,
 - в enum-е :doc:`AttachmentType <proto/Entity message>` элемент ``ResolutionChainAssignment`` переименован в ``ResolutionRouteAssignment``,
 - в структуре :doc:`proto/MessagePatchToPost` поле ``ResolutionChainAssignments`` переименовано в ``ResolutionRouteAssignments``,
 - структура ``ResolutionChainAssignment`` переименована в :doc:`ResolutionRouteAssignment <proto/MessagePatchToPost>`,
 - в структуре :doc:`ResolutionRouteAssignment <proto/MessagePatchToPost>` поле ``ChainId`` переименовано в ``RouteId``,
 - структура ``ResolutionChainList`` переименована в :doc:`ResolutionRouteList <proto/ResolutionRoute>`,
 - в структуре :doc:`ResolutionRouteList <proto/ResolutionRoute>` поле ``ResolutionChains`` переименовано в ``ResolutionRoutes``,
 - структура ``ResolutionChain`` переименована в :doc:`ResolutionRoute <proto/ResolutionRoute>`,
 - в структуре :doc:`ResolutionRoute <proto/ResolutionRoute>` поле ``ChainId`` переименовано в ``RouteId``,
 - метод ``GetResolutionChainsForOrganization`` переименован в :doc:`http/GetResolutionRoutesForOrganization`.


24.03.2017
----------

- Добавлены методы для парсинга титулов УКД: :doc:`продавца <http/utd/ParseUniversalCorrectionDocumentSellerTitleXml>` и :doc:`покупателя <http/utd/ParseUniversalCorrectionDocumentBuyerTitleXml>`.


15.03.2017
----------
**SDK**: `C# 1.39 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions/1.39>`__ | `Java 1.39 <https://github.com/diadoc/diadocsdk-java/releases/tag/versions/1.39>`__ | `C++ 1.39 <https://github.com/diadoc/diadocsdk-cpp/releases/tag/versions/1.39>`__

- Добавлена новая версия метода :doc:`/V5/GetNewEvents /<http/GetNewEvents>` для получения ленты событий по ящику. Основное отличие версии *V5* от версии *V4* в том, что новая версия метода работает для всех пользователей в ящике. Лента событий формируется по подразделению организации, в котором состоит пользователь. Подробнее в описании метода :doc:`http/GetNewEvents`.


10.02.2017
----------
**SDK**: `C# 1.38.3 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions/1.38.3>`__

- В структуре :doc:`OrganizationWithCounteragentStatus <proto/GetOrganizationsByInnListRequest>` добавлено поле ``LastEventTimestampTicks``.


23.12.2016
----------

- Добавлена возможность работать с новыми типами документов УПД и УКД, в связи с чем в документацию добавлены разделы, описывающие:

 - :doc:`документооборот счетов-фактур <docflows/InvoiceDocflow>`,
 - :doc:`документооборот накладных <docflows/Torg12Docflow>`,
 - :doc:`документооборот актов <docflows/AktDocflow>`,
 - :doc:`документооборот УПД/УКД <docflows/UtdDocflow>`,
 - методы и структуры для работы с :doc:`УПД <API_UniversalTransferDocument>`.
 
- Добавлены методы:

 - :doc:`http/utd/GenerateUniversalTransferDocumentXmlForSeller` — генерация титула продавца УПД и УКД,
 - :doc:`http/utd/GenerateUniversalTransferDocumentXmlForBuyer` — генерация титула покупателя УПД и УКД,
 - :doc:`http/utd/ParseUniversalTransferDocumentSellerTitleXml` — парсинг титула продавца УПД,
 - :doc:`http/utd/ParseUniversalTransferDocumentBuyerTitleXml` — парсинг титула покупателя УПД,
 - :doc:`http/utd/ExtendedSignerDetailsV2` — заполнение дополнительных данных (для УПД и УКД) о подписантах.
 
- Добавлены структуры:

 - :doc:`proto/utd/UniversalTransferDocumentSellerTitleInfo` — для описания титула продавца УПД,
 - :doc:`proto/utd/UniversalTransferDocumentBuyerTitleInfo` — для описания титула покупателя УПД,
 - :doc:`proto/utd/UniversalCorrectionDocumentSellerTitleInfo` — для описания титула продавца УКД,
 - :doc:`proto/utd/UniversalTransferDocumentBuyerTitleInfo` — для описания титула покупателя УКД,
 - :doc:`proto/utd/UniversalDocumentMetadata` — для описания данных УПД и УКД,
 - :doc:`proto/utd/ExtendedOrganizationInfo` — для описания реквизитов продавца, покупателя и грузоотправителя, используемая в УПД и УКД,
 - :doc:`proto/utd/ExtendedSigner` — для описания реквизитов подписанта, используемая в УПД и УКД,
 - :doc:`proto/utd/ExtendedSignerDetailsToPost` — для описания реквизитов подписанта, используемая в методе :doc:`proto/utd/ExtendedOrganizationInfo`.
 
- В структуре :doc:`proto/MessageToPost` добавлено поле ``UniversalTransferDocumentSellerTitles``:

 - для отправки УПД с функцией СЧФ,
 - для отправки УКД с функцией КСЧФ,
 - для отправки титула продавца УПД с функцией ДОП и СЧФДОП,
 - для отправки титула продавца УКД с функцией ДОП и СЧФДОП.
 
- Для отправки титула покупателя УПД и УКД в структуре :doc:`proto/MessageToPost` добавлено поле ``UniversalTransferDocumentBuyerTitles``:

 - для отправки титула покупателя УПД с функцией ДОП и СЧФДОП,
 - для отправки титула покупателя УКД с функцией ДОП и СЧФДОП.
 
- В структуре :doc:`proto/PrepareDocumentsToSignRequest` добавлена возможность указать расширенные данные о подписанте.
- В DocflowAPI внесены следующие изменения:

 - добавлены структуры для описания документооборота УПД:
 
  - :doc:`proto/utd/docflow/InboundUniversalTransferDocumentDocflow` — входящий УПД,
  - :doc:`proto/utd/docflow/OutboundUniversalTransferDocumentDocflow` — исходящий УПД,
  - :doc:`proto/utd/docflow/UniversalTransferDocumentInfo` — дополнительные данные о УПД,
  - :doc:`proto/utd/docflow/UniversalCorrectionDocumentInfo` — дополнительные данные о УКД;
  
 - в структуре :doc:`proto/Docflow` добавлены поля ``InboundUniversalTransferDocumentDocflow`` и ``OutboundUniversalTransferDocumentDocflow``;
 - в структуре :doc:`proto/DocumentInfo` добавлены поля ``UniversalTransferDocumentInfo`` и ``UniversalCorrectionDocumentInfo``.


10.10.2016
----------
**SDK**: `C# 1.37 <https://github.com/diadoc/diadocsdk-csharp/releases/tag/versions/1.37>`__

- Добавлена структура :doc:`CustomDocumentAttachment <proto/DocumentAttachment>` для отправки кастомных типов документов.

.. note::
	Функциональность находится в разработке.


07.04.2016
----------

- В метод :doc:`http/GetOrganizationsByInnKpp` добавлен параметр ``includeRelations``, который позволяет получить данные о количестве запросов на поиск и приглашения к сотрудничеству для данной организации.


25.03.2016
----------

- Добавлена возможность авторизации по логину/паролю и сертификату с ключом, полученным доверенным сервисом. Подробности в описании методов :doc:`http/Authenticate` и :doc:`http/AuthenticateConfirm`).


10.03.2016
----------

- Добавлена возможность редактировать пакеты документов:

 - в структуре :doc:`proto/MessagePatchToPost` добавлено поле ``EditDocumentPacketCommands``;
 - добавлена структура :doc:`EditDocumentPacketCommand <proto/MessageToPost>`, описывающая операцию редактирования пакета документов.

 
10.02.2016
----------

- Добавлен метод :doc:`http/GetDepartment`, позволяющий получить информацию о конкретном подразделении организации.


19.01.2016
----------

- Значения перечисления ``ResolutionType`` (:doc:`proto/Resolution`) синхронизированы со значениями, возвращаемые с сервера (значение ``Undefined`` заменено на ``UndefinedResolutionType``).
- В структуре :doc:`proto/MessageToPost` добавлен флаг залоченного пакета ``LockPacket``.


02.12.2015
----------

- В структуре :doc:`proto/Document` добавлено свойство с сообщением об ошибке при доставке в роуминг ``RoamingNotificationStatusDescription``.
- Добавлены новые версии методов :doc:`http/GetCounteragent` и :doc:`http/GetCounteragents`, в которых изменилась логика показа видимых подразделений.


11.11.2015
----------

- В структуре :doc:`proto/Document` добавлено свойство «признак прочитанности» ``IsRead`` .
- Метод :doc:`http/GetDocuments` теперь позволяет искать непрочитанные документы.


14.10.2015
----------

- Добавлена возможность отправлять новый тип документа «Дополнительное соглашение к договору»:

 - в структуре :doc:`proto/MessageToPost` добавлена стуктура :doc:`proto/SupplementaryAgreementAttachment` для передачи дополнительного соглашения к договору;
 - в структуры :doc:`proto/Entity message` и :doc:`proto/DocumentType` добавлен новый тип для дополнительного соглашения к договору;
 - в структуре :doc:`proto/Document` добавлена вложенная структура :doc:`SupplementaryAgreementMetadata <proto/BilateralDocumentMetadata>` для описания метаданных дополнительного соглашения к договору;
 - в структуре :doc:`proto/DocumentInfo` добавлена вложенная структура :doc:`SupplementaryAgreementInfo <proto/SupplementaryAgreementDocumentInfo>` для описания метаданных дополнительного соглашения к договору.


10.08.2015
----------

- Добавлена возможность отправлять зашифрованные товарные накладные и акты выполненных работ:

 - в структуре :doc:`proto/MessageToPost` добавлены поля ``EncryptedXmlTorg12SellerTitles`` и ``EncryptedXmlAcceptanceCertificateSellerTitles``;
 - добавлена структура :doc:`proto/EncryptedXmlDocumentAttachment` для передачи зашифрованных накладных и актов.


10.08.2015
----------

- В метод :doc:`http/GetMyOrganizations` добавлен параметр ``autoRegister``, который позволяет управлять автоматической регистрацией пользователя с сертификатом КЭП в организации.


30.07.2015
----------

- Добавлена возможность отправлять зашифрованные счета-фактуры:

 - добавлены структуры :doc:`CounteragentCertificateList <proto/Counteragent>` и :doc:`Certificate <proto/Counteragent>` для описания списка сертификатов контрагента;
 - в структурах :doc:`proto/Document` и :doc:`proto/Entity message` добавлен флаг ``IsEncryptedContent``:— он указывается для передачи контента в зашифрованном виде;
 - добавлены структуры для передачи зашифрованных счетов-фактур и метаданных для исправлений и корректировок:
 
  - :doc:`proto/EncryptedInvoiceAttachment`
  - :doc:`EncryptedDocumentMetadata <proto/EncryptedInvoiceAttachment>`
  - :doc:`EncryptedInvoiceMetadata <proto/EncryptedInvoiceAttachment>`
  - :doc:`EncryptedInvoiceCorrectionMetadata <proto/EncryptedInvoiceAttachment>`
  
 - в структуре :doc:`proto/MessageToPost` добавлено поле ``EncryptedInvoices`` для передачи зашифрованных счетов-фактур;
 - в структуре :doc:`proto/MessagePatchToPost` добавлено поле ``SignatureVerifications`` для передачи резльтатов проверки подписей на стороне получателя;
 - добавлен метод :doc:`http/GetCounteragentCertificates` для запроса списка сертификатов контрагента;
 - в структуре :doc:`proto/Signer` добавлен отпечаток сертификата ``SignerCertificateThumbprint``.
 
- Добавлена возможность изменения подписанта в неотправленных исходящих документах:

 - добавлена структура :doc:`DocumentToPatch <proto/PrepareDocumentsToSignRequest>`, представляющая изменение исходящего неотправленного документа;
 - изменились структуры :doc:`proto/DocumentSignature`, :doc:`proto/PrepareDocumentsToSignRequest`: в них добавлена возможность ссылаться на изменение исходящего неотправленного документа.

 
28.05.2015
----------

- Добавлен метод :doc:`http/GetResolutionRoutesForOrganization` для получения списка цепочек согласования организации. Изменен протобуфер :doc:`proto/MessagePatchToPost`: добавлена структура ``ResolutionChainAssignment`` для постановки документа на цепочку согласования.


25.05.2015
----------

- Добавлен метод :doc:`http/GenerateForwardedDocumentPrintForm` для получения печатной формы со штампом для пересланного документа.


28.04.2015
----------

- Добавлен метод :doc:`http/Authenticate` для аутентификации по ключу, полученному доверенным сервисом.


13.04.2015
----------

- Изменены структуры :doc:`proto/InvoiceInfo` и :doc:`proto/InvoiceCorrectionInfo`, которые предоставляют исходные данные для формирования СФ и КСФ в XML-формате с помощью метода :doc:`http/GenerateInvoiceXml`.
- Добавлена возможность указывать версию формата СФ и КСФ и указывать поля, соответствующие новой версии XML-формата СФ.
- Изменилась логика работы метода :doc:`http/ParseInvoiceXml` в зависимости от формата СФ.

.. warning::
 Версия сборки SDK не изменилась. Всем, кто скачал сборку в период с 10.04.2015-12.04.2015, необходимо скачать свежую сборку от 13.04.2015.


10.04.2015
----------

- Изменены структуры :doc:`proto/InvoiceInfo` и :doc:`proto/InvoiceCorrectionInfo`, которые предоставляют исходные данные для формирования СФ и КСФ в XML-формате с помощью метода :doc:`http/GenerateInvoiceXml`.
- Добавлена возможность указывать версию формата СФ и КСФ.


02.04.2015
----------

- Добавлена возможность отравлять приглашения организациям, не подключенным к Диадоку. Соответствующие изменения внесены в методы :doc:`http/AcquireCounteragent` и :doc:`http/AcquireCounteragentResult`. Старая версия метода :doc:`http/AcquireCounteragent` через некоторое время будет отключена.


20.01.2015
----------

- Добавлены методы для работы с :doc:`Контур.Сертификатом<CloudSignApi>`.


15.10.2014
----------

- Добавлен метод :doc:`http/GenerateDocumentZip`, позволяющий формировать zip-архив с документом, подписями к нему и файлами документооборота.


02.10.2014
----------

- Добавлена возможность привязывать к документам произвольные данные «ключ-значение». Соответствующие изменения внесены в структуры :doc:`proto/MessageToPost` и :doc:`proto/MessagePatchToPost`.


05.06.2014
----------

- Добавлена возможность получать статус доставки документа в роуминг: :doc:`proto/RoamingNotification`.


25.02.2014
----------

- Добавлена поддержка новых типов полуформализованных документов:

 - :doc:`протокол согласования цены <proto/NonformalizedAttachment>`
 - :doc:`реестр сертификатов <proto/NonformalizedAttachment>`
 - :doc:`акт сверки <proto/ReconciliationActAttachment>`
 - :doc:`договор <proto/ContractAttachment>`
 - :doc:`детализация <proto/ServiceDetailsAttachment>`
 - :doc:`накладная ТОРГ-13 <proto/Torg13Attachment>`
 

05.02.2014
----------

- Добавлена возможность получать через API протокол передачи документа с помощью метода :doc:`http/GenerateDocumentProtocol`. Выгрузка протокола передачи документа адресатом пересылки документа третьей стороне производится с помощью метода :doc:`http/GenerateForwardedDocumentProtocol`.


24.01.2014
----------

- Добавлена возможность пересылать документы третьей стороне. Подробнее в описании методов:

 - :doc:`http/ForwardDocument`
 - :doc:`http/GetForwardedDocuments`
 - :doc:`http/GetForwardedDocumentEvents`.
 
 Выгрузка содержимого сущностей, связанных с документом, адресатом пересылки документа третьей стороне производится с помощью метода :doc:`http/GetForwardedEntityContent`.


20.12.2013
----------

- Сборка protobuf-net.dll теперь внедрена в библиотеку DiadocApi.dll. Это позволяет интегратору использовать в своем проекте другую версию сборки protobuf-net.dll.


06.12.2013
----------

- Добавлена возможность отправлять формализованные отказы от подписи документов. Xml-файл отказа формируется с помощью метода :doc:`http/GenerateSignatureRejectionXml`.

 - Для отправки отказов используется метод :doc:`http/PostMessagePatch`, в который передается структура :doc:`proto/MessagePatchToPost` с заполненным списком :doc:`MessagePatchToPost.XmlSignatureRejections <proto/MessagePatchToPost>`.
 - Для получения документов с отказом в подписи через метод :doc:`http/GetDocuments` используются такие же фильтры, как для неформализованных отказов. Формализованным отказам соответствует тип ``XmlSignatureRejection`` из перечисления :doc:`AttachmentType <proto/Entity message>`.
 
- Отправка неформализованных отказов от подписи в адрес роуминговых организаций теперь запрещена.
- Новые отказы от подписи, при получении их через старые версии SDK, будут иметь тип :doc:`SignatureRequestRejection <proto/Entity message>`, — как отказы старого формата, — но в содержимом соответствующих сущностей вместо строки с комментарием к отказу теперь будет возвращаться xml файл отказа в кодировке CP1251.


20.10.2013
----------

- Добавлена возможность аннулирования документов.

 - Для отправки предложения об аннулировании через API при обращении к методу :doc:`http/PostMessagePatch` заполните список :doc:`MessagePatchToPost.RevocationRequests <proto/MessagePatchToPost>`. Каждый элемент этого списка представляет собой структуру :doc:`RevocationRequestAttachment <proto/MessagePatchToPost>`.
 - Для принятия предложения об аннулировании через API при обращению к методу :doc:`http/PostMessagePatch` заполните список :doc:`MessagePatchToPost.RequestedSignatures <proto/MessagePatchToPost>`.
 - Для отказа от предложения об аннулировании через API при обращении к методу :doc:`http/PostMessagePatch` заполните список :doc:`MessagePatchToPost.XmlSignatureRejections <proto/MessagePatchToPost>`. Каждый элемент этого списка представляет собой структуру :doc:`XmlSignatureRejectionAttachment <proto/MessagePatchToPost>`.
 - При получение информации о документах через API с помощью методов :doc:`http/GetMessage`, :doc:`http/GetDocument` и т.п. для любых документов в структуре :doc:`proto/Document` заполняется поле :doc:`RevocationStatus <proto/Document>`.
 
- Добавлены методы :doc:`http/GenerateRevocationRequestXml` и :doc:`http/GenerateSignatureRejectionXml`, облегчающие процесс формирования корректных XML файлов предложения об аннулировании и формализованного отказа в подписи.
- Добавлены методы :doc:`http/ParseRevocationRequestXml` и :doc:`http/ParseSignatureRejectionXml`, позволяющие преобразовывать xml-файлы предложения об аннулировании и формализованного отказа в подписи в структуры :doc:`proto/RevocationRequestInfo` и :doc:`proto/SignatureRejectionInfo` соответственно.


13.08.2013
----------

- Изменены методы по работе со списками контрагентов. Подробнее в описании методов:

 - :doc:`http/GetCounteragents`
 - :doc:`http/AcquireCounteragent`
 - :doc:`http/BreakWithCounteragent`


10.04.2013
----------

- Добавлена поддержка нового типа полуформализованных документов — ценовых листов. Ценовой лист представляет собой двусторонний документ (для него требуется подпись контрагента/отказ в запросе подписи) со следующими обязательными реквизитами:

 - дата составления и номер самого ценового листа
 - дата вступления ценового листа в силу
 - дата и номер договора, к которому относится ценовой лист.
 
Для отправки ценовых листов через API при обращении к методу :doc:`http/PostMessage` заполните список :doc:`MessageToPost.PriceLists <proto/MessageToPost>`. Каждый элемент этого списка представляет собой структуру :doc:`proto/PriceListAttachment`.
При получение информации о документах через API с помощью методов :doc:`http/GetMessage`, :doc:`http/GetDocument` и т.п. для ценовых листов в структуре :doc:`proto/Document` заполняется поле :doc:`PriceListMetadata <proto/BilateralDocumentMetadata>`.
При фильтрации документов методом :doc:`http/GetDocuments` можно использовать новый тип документов ``PriceList``.
- Для получения списка пользователей конкретной организации добавлен метод :doc:`http/GetOrganizationUsers`.
- В структуре :doc:`proto/Organization` добавлено поле ``IfnsCode``, позволяющее получить код налоговой инспекции — место подачи декларации по НДС.


14.03.2013
----------

- Добавлена возможность отправлять документы, подписанные тестовой подписью с помощью флага :doc:`SignedContent.SignWithTestSignature <proto/SignedContent>`.
- Добавлены методы :doc:`http/ParseAcceptanceCertificateSellerTitleXml` и :doc:`http/ParseTorg12SellerTitleXml`, позволяющие преобразовывать xml-файлы формализованных актов (титул исполнителя) и ТОРГ-12 (титул продавца) в структуры :doc:`AcceptanceCertificateSellerTitleInfo <proto/AcceptanceCertificateInfo>` и :doc:`Torg12SellerTitleInfo <proto/Torg12Info>` соответственно.
- Расширена функциональность метода :doc:`http/PostMessage`: с помощью флага :doc:`MessageToPost.DelaySend <proto/MessageToPost>` можно задержать отправку документа, чтобы была возможность провести его согласование. В связи с этим изменился набор возможных состояний документов, что требует обновления логики клиентских решений.
- Чтобы определить, может ли пользователь запрашивать согласования, используйте флаг :doc:`OrganizationUserPermissions.CanRequestResolutions <proto/OrganizationUserPermissions>` в свойствах пользователя, возвращаемых методом :doc:`http/GetMyPermissions`.
- В сообщение :doc:`EntityPatch <proto/MessagePatch>` добавлено поле ``ContentIsPatched``, через которое сервер выдает информацию о том, что исходный документ в процессе подписания был модифицирован. В документ была внедрена информация о том, кто подписал этот документ.
- Изменена логика работы с перечислимыми типами: теперь в большинстве перечислений имеется специальное значение с именем ``UnknownИмяПеречисления``. Клиент получит такое значение только том случае, если есть рассогласование версий API между клиентом и сервером, и клиент не может правильно интерпретировать информацию, возвращаемую сервером (например, в случае добавления новых элементов к перечислению клиент будет получать вместо вновь добавленных элементов значение ``UnknownИмяПеречисления``). Клиент должен корректно обрабатывать такие ситуации, например, путем информирования пользователя о необходимости обновить интеграционный модуль.

.. warning::
 Для доступа к новой функциональности и во избежание возможного конфликта версий обновите `SDK <https://diadoc.kontur.ru/sdk/>`__.


31.01.2013
----------

- Добавлена возможность работы с документами, пересылаемыми внутри организации:

 - добавлены элементы в перечислениях :doc:`NonformalizedDocumentStatus <proto/NonformalizedDocumentMetadata>`, :doc:`BilateralDocumentStatus <proto/BilateralDocumentMetadata>` и :doc:`UnilateralDocumentStatus <proto/UnilateralDocumentMetadata>`;
 - добавлены поля для работы с подразделениями организации в структурах :doc:`proto/Department`, :doc:`Entity <proto/Entity message>`, :doc:`proto/Document`, :doc:`proto/Message` и :doc:`proto//MessageToPost`.
 
- Расширены возможности работы с «черновиками», то есть с подготовленными, но не отправленными документами:

 - для отправки ранее созданного черновика добавился метод :doc:`http/SendDraft`;
 - черновики теперь можно загружать в Диадок с помощью метода :doc:`http/PostMessage` — это предпочтительный способ;
 - изменилась структура :doc:`proto//MessageToPost`;
 - добавлена структура :doc:`proto/DraftToSend`;
 - структура ``RequestedSignature`` переименована в ``DocumentSignature``, подробнее в описании :doc:`proto/MessagePatchToPost`.
 
- Добавлена возможность загружать большие по размеру документы в Диадок с помощью сервиса «полки документов». Для этих целей добавился метод :doc:`http/ShelfUpload` и обновилась структура :doc:`proto/SignedContent`, в которой добавлено поле ``NameOnShelf``, позволяющее сослаться на уже загруженный на «полку» файл.
- Добавлена возможность восстанавливать ранее удаленные отдельные документы и сообщения целиком. Для этих целей добавлен метод :doc:`http/Restore`, а в структурах :doc:`EntityPatch <proto/MessagePatch>` и :doc:`proto/MessagePatch` добавлены поля, позволяющие узнать, были ли конкретный документ или сообщение восстановлены.
- Добавлена возможность по :doc:`документу <proto/Document>` или :doc:`сообщению <proto/Message>` понять, является ли он юридически значимым. Для этих целей в каждую из названных структур добавлено поле ``IsTest``.
- Добавлена возможность проводить эвристический семантический разбор строк, представляющих почтовый адрес в Российской Федерации. За это отвечает метод :doc:`http/ParseRussianAddress`.
- Добавлена возможность выполнять трансформацию XML-файла СФ/ИСФ, сформированного в соответствии с :download:`XML-схемой <xsd/ON_SFAKT_1_897_01_05_01_02.xsd>`, в структуру :doc:`proto/InvoiceInfo`. За это отвечает метод :doc:`http/ParseInvoiceXml`.


29.08.2012
----------

- В структуре :doc:`proto/Organization` добавлено поле ``Departments``, содержащее список всех подразделений в организации. Это поле позволяет получать информацию об оргструктуре с помощью методов :doc:`http/GetMyOrganizations`, :doc:`http/GetOrganization`, :doc:`http/GetCounteragents`, :doc:`http/GetCounteragent`.
- В методах :doc:`http/PostMessage` и ``PostDraft`` добавлена возможность отправлять документы в конкретное подразделение контрагента:

 - в структуре :doc:`proto/MessageToPost` добавлено новое поле ``ToDepartmentId``;
 - в метод ``PostDraft`` добавлен новый параметр ``toDepartmentId``.
 
- Добавлен метод :doc:`http/MoveDocuments` для перемещения документов своей организации между подразделениями. Информация о перемещениях документов между подразделениями, — неважно было это сделано через API или через Web, — доступна через метод :doc:`http/GetNewEvents`.
- В структуре :doc:`EntityPatch <proto/MessagePatch>` добавлено поле ``MovedToDepartmentId``.
- В структуре :doc:`Entity <proto/Entity message>` добавлено поле ``RawCreationDate``, содержащее :doc:`метку времени <proto/Timestamp>` создания сущности. Это поле заполняется для всех сущностей, его можно использовать для получения времени подписания или согласования документа.
- Добавлена возможность осуществлять согласование или отказ в согласовании документов через API:

 - добавлена структура :doc:`proto/Resolution`;
 - в структуре :doc:`proto/MessagePatchToPost` добавлено поле ``Resolutions``;
 - все действия по согласованию видны в структуре :doc:`proto/Message` как сущности с типом :doc:`Attachment/Resolution <proto/Entity message>`; содержимое этой сущности — байты строки комментария к согласованию в кодировке UTF-8;
 - в структуре :doc:`Entity <proto/Entity message>` добавлено поле ``ResolutionInfo``, содержащее тип действия по согласованию и ФИО согласователя в виде новой структуры :doc:`ResolutionInfo <proto/Resolution>`.


26.06.2012
----------

- Добавлен метод :doc:`http/Delete`, который помечает документы как удаленные.
- В структурах :doc:`proto/Document` и :doc:`proto/Message` добавлены флаги ``IsDeleted``.
- В структуре :doc:`proto/MessagePatch` добавлен флаг ``MessageIsDeleted`` и поле ``EntityPatches``, содержащее список структур типа ``EntityPatch`` с флагом ``DocumentIsDeleted``. Эти изменения структуры MessagePatch позволяют отслеживать моменты удаления документов и/или сообщений, анализируя поток событий в ящике, возвращаемый методом :doc:`http/GetNewEvents`.
- Добавлен метод :doc:`http/CanSendInvoice`, позволяющий для данного идентификатора ящика и сертификата ЭП узнать, был ли этот сертификат зарегистрирован в ФНС в качестве сертификата, используемого для подписания электронных счетов-фактур, отправляемых участником ЭДО, которому принадлежит данный ящик в Диадоке. Т.е. метод ``CanSendInvoice`` отвечает на вопрос, может ли тот или иной сертификат ЭП использоваться для подписания ЭСФ, отправляемых из данного ящика.
- В структуре :doc:`proto/Organization` добавлено поле ``FnsRegistrationDate`` — дата подачи заявления в ФНС на регистрацию данной организации в качестве участника документооборота ЭСФ.
- Метод ``PostDraft`` теперь позволяет загружать в черновики товарные накладные и акты о выполнении работ/оказании услуг в рекомендованном ФНС XML-формате (документы с типами :doc:`Attachment/XmlTorg12 <proto/Entity message>` и :doc:`Attachment/XmlAcceptanceCertificate <proto/Entity message>`). Также в метод ``PostDraft`` добавлена поддержка счетов на оплату (документов типа :doc:`Attachment/ProformaInvoice <proto/Entity message>`).


09.06.2012
----------
**v1.2**

- Расширен перечень сведений, возвращаемых методами, дающими доступ к справочнику организаций в Диадоке, например, :doc:`http/GetMyOrganizations`. Теперь структура :doc:`proto/Organization` включает поля:

 - ``Ogrn`` — ОГРН организации;
 - ``Address`` — юридический адрес организации;
 - ``FnsParticipantId`` — уникальный идентификатор участника документооборота СФ, который должен указываться при формировании XML счетов-фактур.
 
- Метод :doc:`http/GenerateInvoiceXml` теперь формирует не только XML-файлы счетов-фактур, но и XML-файлы исправлений счетов-фактур, корректировочных счетов-фактур и исправлений корректировочных счетов-фактур.


11.05.2012
----------
**v1.1**

- Добавлена поддержка рекомендованных ФНС России форматов электронных товарных накладных и актов о выполнении работ/оказании услуг. Теперь с помощью метода :doc:`http/PostMessage` можно загружать в Диадок титулы продавца XML-накладных (новый тип документов :doc:`Attachment/XmlTorg12 <proto/Entity message>`) и титулы исполнителя XML-актов (новый тип документов :doc:`Attachment/XmlAcceptanceCertificate <proto/Entity message>`), а с помощью метода :doc:`http/PostMessagePatch` можно загружать в Диадок соответствующие титулы покупателя/заказчика. В SDK включены XML-схемы, описывающие рекомендованные ФНС России форматы товарных накладных и актов о выполнении работ/оказании услуг:

 - :download:`XML-схема товарной накладной, титул продавца <xsd/DP_OTORG12_1_986_00_05_01_02.xsd>`
 - :download:`XML-схема товарной накладной, титул покупателя <xsd/DP_PTORG12_1_989_00_05_01_02.xsd>`
 - :download:`XML-схема акта о выполнении работ/оказании услуг, титул исполнителя <xsd/DP_IAKTPRM_1_987_00_05_01_02.xsd>`
 - :download:`XML-схема акта о выполнении работ/оказании услуг, титул заказчика <xsd/DP_ZAKTPRM_1_990_00_05_01_02.xsd>`
 
- Добавлены методы, облегчающие процесс формирования корректных XML-файлов товарных накладных и актов:

 - :doc:`http/GenerateTorg12XmlForSeller`
 - :doc:`http/GenerateTorg12XmlForBuyer`
 - :doc:`http/GenerateAcceptanceCertificateXmlForSeller`
 - :doc:`http/GenerateAcceptanceCertificateXmlForBuyer`
 
 А в метод :doc:`http/GetDocuments` добавлена поддержка новых типов документов.
 
- Добавлена возможность с помощью метода :doc:`http/PostMessage` загружать в Диадок счета на оплату (новый тип документов :doc:`Attachment/ProformaInvoice <proto/Entity message>`). Поддержка данного типа документов добавлена и в метод :doc:`http/GetDocuments`.
- В метод :doc:`http/PostMessage` добавлена возможность загружать в Диадок вложения специального типа «структурированные данные» :doc:`Attachment/StructuredData <proto/Entity message>`, с помощью которого можно организовать передачу рядом с юридически-значимой печатной формой документа каких-то данных, подлежащих автоматизированной обработке.
- Метод :doc:`http/GetDocuments` теперь позволяет получать информацию обо всех СФ-подобных документах (СФ/ИСФ/КСФ/ИКСФ) единым списком. Для этого в качестве первой части параметра ``filterCategory`` нужно передать специальное значение ``AnyInvoiceDocumentType``. Например, чтобы получить список всех входящих СФ/ИСФ/КСФ/ИКСФ, нужно в метод ``GetDocuments`` передать параметр ``filterCategory=AnyInvoiceDocumentType.Inbound``.


04.04.2012
----------

- Добавлена поддержка официально утвержденных версий форматов документов, фигурирующих в документообороте счетов-фактур. В связи с этим поменялись сигнатуры методов :doc:`http/GenerateInvoiceDocumentReceiptXml` и :doc:`http/GenerateInvoiceCorrectionRequestXml`. В SDK включены соответствующие XML-схемы, описывающие форматы документов, фигурирующих в документообороте счетов-фактур:

 - :download:`XML-схема счета-фактуры (СФ) <xsd/ON_SFAKT_1_897_01_05_01_02.xsd>`, эта же схема описывает формат исправления СФ (ИСФ);
 - :download:`XML-схема корректировочного счета-фактуры (КСФ) <xsd/ON_KORSFAKT_1_911_01_05_01_02.xsd>`, эта же схема описывает формат исправления КСФ (ИКСФ);
 - :download:`XML-схема извещения о получении документа <xsd/DP_IZVPOL_1_982_00_01_01_02.xsd>`;
 - :download:`XML-схема подтверждения оператора о дате отправки СФ/ИСФ/КСФ/ИКСФ <xsd/DP_PDPOL_1_984_00_01_01_02.xsd>` (выдается продавцу);
 - :download:`XML-схема подтверждения оператора о дате доставки СФ/ИСФ/КСФ/ИКСФ <xsd/DP_PDOTPR_1_983_00_01_01_02.xsd>` (выдается покупателю);
 - :download:`XML-схема уведомления об уточнении СФ/ИСФ/КСФ/ИКСФ <xsd/DP_UVUTOCH_1_985_00_01_01_02.xsd>` (формируется покупателем).
 
 Для обеспечения обратной совместимости с существующими пилотными проектами по итеграции Диадок в течение еще какого-то времени будет продолжать принимать счета-фактуры в старом формате. Однако такие документы не будут иметь юридической значимости.
 
- Добавлен метод :doc:`http/GenerateInvoiceXml`, который облегчает процесс формирования корректного XML-файла счета-фактуры. Метод позволяет интегратору не погружаться в детали XML-формата СФ, а передавать в Диадок только необходимые первичные данные в виде структуры :doc:`proto/InvoiceInfo`. По этим данным метод ``GenerateInvoiceXml``, при необходимости дополнив их сведениями из своих справочников, сформирует корректный XML-файл счета-фактуры, который затем можно будет отправить методом :doc:`http/PostMessage` или загрузить в черновики методом ``PostDraft``. В структуре ``InvoiceInfo`` можно не заполнять реквизиты продавца и покупателя: достаточно указать идентификаторы их ящиков в Диадоке, и соответствующие реквизиты будут подставлены из справочника организаций Диадока.

- Добавлена возможность работать с исправлениями счетов-фактур и корректировочными счетами-фактурами. Для этого введены :doc:`типы сущностей <proto/Entity message>`:

 - ``Attachment/InvoiceRevision`` — исправление счета-фактуры;
 - ``Attachment/InvoiceCorrection`` — корректировочный счет-фактура;
 - ``Attachment/InvoiceCorrectionRevision`` — исправление корректировочного счета-фактуры.
 
 Для связывания исправлений и корректировок с оригинальными СФ нужно использовать уже имеющийся в Диадоке механизм установки ссылок между документами, находящимися в разных сообщениях. Кроме того, в структуре :doc:`Document.InvoiceMetadata <proto/InvoiceDocumentMetadata>`, описывающей метаданные счета-фактуры в Диадоке, добавлено поле ``InvoiceAmendmentFlags``, которое отражает статус счета-фактуры с точки зрения наличия уведомления об уточнении или отправленного исправления/корректировки. Например, при отправке корректировочного счета-фактуры, у исходного счета-фактуры, по которому было запрошено уточнение, поле ``Document.InvoiceMetadata.InvoiceAmendmentFlags`` поменяет свое значение с ``AmendmentRequested`` на ``AmendmentRequested\Corrected``.
 
- Добавлен метод :doc:`http/GetInvoiceCorrectionRequestInfo`, который возвращает информацию, содержащуюся в уведомлении об уточнении счета-фактуры, без необходимости уметь разбирать соответствующий XML-формат, утвержденный ФНС, что в какой-то степени упрощает работу интегратора. В частности, метод ``GetInvoiceCorrectionRequestInfo`` позволяет получить текст уведомления об уточнении.
- Добавлены методы :doc:`http/PostMessage` и ``PostDraft`` позволяющие загружать в Диадок акты о выполнении работ/оказании услуг (новый тип документов :doc:`Attachment/AcceptanceCertificate <proto/Entity message>`). Поддержка нового типа документов добавлена и в метод :doc:`http/GetDocuments`.
- Метод :doc:`http/GetDocuments` теперь возволяет фильтровать список документов по дате формирования документа в учетной системе (реквизиту самого документа), а не только по дате загрузки документа в Диадок. Для этого в метод ``GetDocuments`` добавлены необязательные параметры строки запроса ``fromDocumentDate`` и ``toDocumentDate``, которые позволяют задать интервал времени, в котором осуществляется поиск. При этом метод ``GetDocuments`` продолжает поддерживать фильтрацию списка документов с помощью параметров ``timestampFromTicks`` и ``timestampToTicks``.
- Доработаны методы для работы с черновиками:

 - Метод :doc:`http/GetNewEvents` теперь возвращает информацию о событиях, происходящик с черновиками: создание черновика и начальный набор документов в нем, добавление к черновику документов, утилизация черновика (просто удаление, либо отправка на основе него полноценного сообщения).
 - Методы :doc:`http/GetEvent` и :doc:`http/GetMessage` теперь возвращают информацию о черновиках.
 - Метод :doc:`http/RecycleDraft` удаляет еще неотправленные черновики.
 - В сообщение :doc:`proto/Message` добавлено необязательное поле ``CreatedFromDraftId``, в которое заносится идентификатор черновика, на основании которого было создано данное сообщение или черновик.
 - В черновике добавлено поле ``DraftIsTransformedToMessageId``, в которое заносится идентификатор сообщения или черновика, которое было создано из данного черновика. Флаг ``Message.DraftIsRecycled`` означает, что черновик был утилизирован, то есть удален или преобразован в полноценное сообщение или в другой черновик. Поля ``DraftIsTransformedToMessageId`` и ``DraftIsRecycled`` могут присутствовать в структуре ``Message``, описывающей черновик, одновременно.
 - Метод ``PostDraft`` теперь позволяет создать нередактируемые черновики — черновики, которые можно только отправить или удалить. Добавление или удаление документов из таких черновиков заблокировано как в веб-интерфейсе Диадока, так и в API-методе ``PostDraft``. Для создания нередактируемого черновика нужно в метод ``PostDraft`` передать параметр ``lock`` без значения.

 
18.01.2012
----------

- Добавлены методы для управления списком контрагентов:

 - :doc:`http/GetCounteragents` — возвращает список контрагентов, отфильтрованный по их статусу;
 - :doc:`http/GetCounteragent` — возвращает информацию о контрагенте по его идентификатору;
 - :doc:`http/AcquireCounteragent` — добавляет организацию в список своих контрагентов;
 - :doc:`http/BreakWithCounteragent` — исключает организацию из списка своих контрагентов.
 
- Переработан механизм получения справочной информации об организациях и ящиках в Диадоке. Следующие методы объявлены устаревшими и через некоторое время не будут поддерживаться:

 - ``GetBoxInfo`` — вместо него используйте методы :doc:`http/GetOrganization` и :doc:`http/GetBox`, которые возвращают информацию о конкретных организации и ящике по их идентификаторам;
 - ``GetBoxesByInnKpp`` — вместо него используйте метод :doc:`http/GetOrganizationsByInnKpp`, который возвращает информацию о ящиках в Диадоке по ИНН и КПП организации;
 - ``GetBoxesByAuthToken`` — вместо него используйте метод :doc:`http/GetMyOrganizations`, который возвращает информацию об организациях и ящиках, к которым имеет доступ владелец текущего авторизационного токена.


16.12.2011
----------

- Добавлен метод :doc:`http/GetDocuments`, позволяющий быстро получать информацию о документах, например, о счетах-фактурах, в своем ящике, задавая различные критерии фильтрации документов.
- Добавлен метод :doc:`http/GetDocument`, позволяющий получить всю метаинформацию об отдельном документе, зная его идентификатор.
- Добавлена возможность с помощью методов :doc:`http/PostMessage` и ``PostDraft`` загружать в Диадок новые типы докуметов, в частности, товарные накладные (ТОРГ-12) и запросы на инициацию канала обмена документами через Диадок :doc:`TrustConnectionRequest <proto/TrustConnectionRequestAttachment>`.
- В структура :doc:`Entity <proto/Entity message>` добавлено поле ``DocumentInfo``. Для сущности типа ``Attachment`` это поле содержит дополнительную информацию о документе, представляемом этой сущностью.


03.10.2011
----------

- Добавлены методы ``Recognize`` и ``GetRecognized`` для распознавания печатных форм счетов-фактур. Печатная форма подается на вход метода ``Recognize`` в формате `XPS <https://msdn.microsoft.com/en-us/library/windows/hardware/dn641615(v=vs.85).aspx>`__. В случае успешного распознавания на выходе метода ``GetRecognized`` получается XML-файл счета-фактуры в формате, удовлетворяющем требованиям ФНС и пригодном для отправки в соответствии с порядком, утвержденным Минфином РФ.


26.08.2011
----------

- В патчи с уведомлениями о невозможности доставки (DFN), возникающими из-за невалидности подписей под передаваемыми документами, теперь добавляются протоколы проверки подписей в виде отдельных сущностей для каждой подписи. Эти сущности-протоколы имеют тип :doc:`Attachment/SignatureVerificationReport <proto/Entity message>` и привязываться к «своим» подписям с помощью поля ``Entity.ParentEntityId``. Протоколы проверки формируются для всех подписей, — как валидных, так и невалидных, — поэтому чтобы понять, какие именно подписи были признаны недействительными, нужно анализировать содержимое соответствующих протоколов. Содержимое сущности-протокола (массив байтов ``Entity.Content.Data``) представляет собой сериализованную в протобуфер структуру :doc:`proto/SignatureVerificationResult`.


15.08.2011
----------

- Добавлена возможность запрашивать формирование ЭП под пересылаемыми данными «по доверенности». В этом случае изготавливать ЭП на клиенте не нужно (можно не устанавливать на рабочее место криптопровайдер), вместо этого формирование необходимой подписи будет происходить на сервере в момент доставки отправленного сообщения. Изменения отразились в структурах :doc:`proto/MessageToPost` и :doc:`proto/MessagePatchToPost`.


08.07.2011
----------

- Добавлена возможность формирования печатных форм различных документов (в частности счетов-фактур) с помощью метода :doc:`http/GeneratePrintForm`.


17.06.2011
----------

- Добавлена возможность связывать документы в разных сообщениях. Для этого нужно заполнить структуру :doc:`proto/DocumentId`, например, в структуре :doc:`proto/XmlDocumentAttachment` при отправке корректировочного счета-фактуры.
- Добавлена возможность отправить отказ от запрошенной подписи: в структуре :doc:`proto/MessagePatchToPost` добавлено необязательное поле ``RequestedSignatureRejections``.
- Добавлена возможность отслеживания отдельных документов при отправке их через черновики: метод ``PostDraft`` возвращает вместе с идентификатором черновика еще и идентификатор сущности, в которую превращается загруженный документ.
- Уведомления о невозможности доставки теперь ссылаются на недоставленные куски сообщения:

 - в структуре :doc:`Entity <proto/Entity message>` добавлено необязательное поле ``NotDeliveredEventId`` — это идентификатор сообщения или патча, который не удалось доставить (например, из-за некорректности одной или нескольких подписей в нем);
 - получить недоставленный кусок сообщения можно с помощью метода :doc:`http/GetEvent`, передав ему в качестве параметра ``EventId`` значение ``NotDeliveredEventId``. Данное поле заполняется только у сущности типа ``Attachment`` с типом вложения ``DeliveryFailureNotification``.


15.04.2011
----------

- Методы ``GetBoxInfo``, ``GetBoxesByAuthToken`` и ``GetBoxesByInnKpp`` теперь отдают данные в формате XML.


07.04.2011
----------

- Добавлена возможность создавать черновики с помощью метода ``PostDraft``.


30.03.2011
----------

- Добавлена возможность вести документооборот по счетам-фактурам в соответствии с порядком Минфина.


18.02.2011
----------

- Добавлены методы для получения справочной информации ``GetBoxInfo`` и ``GetBoxesByInnKpp``.
- Добавлен метод :doc:`http/GetEntityContent` для получения контента вложений по отдельности.
- Метод :doc:`http/GetMessage` больше не отдает контент свыше 1Мб единовременно. Вместо него используйте метод :doc:`http/GetEntityContent`.


09.12.2010
----------

- Первый релиз интеграторского интерфейса.