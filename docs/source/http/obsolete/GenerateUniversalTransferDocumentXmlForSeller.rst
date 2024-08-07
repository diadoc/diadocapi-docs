GenerateUniversalTransferDocumentXmlForSeller
=============================================

.. warning::
	Метод устарел. Для генерации документов используйте метод :doc:`../GenerateTitleXml`.

Имя ресурса: **/GenerateUniversalTransferDocumentXmlForSeller**

HTTP метод: **POST**

Параметры строки запроса:

-  *documentVersion* - строковый идентификатор версии, уникальный в рамках функции типа документа;
-  *correction* - тип генерируемого документа; принимает одно из значений:

    -  если параметр отсутствует или принимает значение ``correction = false`` - в таком случае метод будет генерировать XML-файл в соответствии со схемой УПД,

    -  если параметр присутствует без значения или принимает значение ``correction = true`` - в таком случае метод будет генерировать XML-файл в соответствии со схемой УКД,

-  *disableValidation* - отключение валидации полученного Xml документа по формату ФНС; параметр может отсутствовать;

В запросе должен присутствовать HTTP-заголовок ``Authorization`` с необходимыми данными для :doc:`авторизации <../../Authorization>`.

В теле запроса должны содержаться данные для изготовления документов в формате УПД или УКД:

-  для УПД в виде сериализованной структуры :doc:`../../proto/obsolete/UniversalTransferDocumentSellerTitleInfo`,

-  для УКД в виде сериализованной структуры :doc:`../../proto/obsolete/UniversalCorrectionDocumentSellerTitleInfo`,

В теле ответа содержится XML-файл, построенный на основании данных из запроса:

-  для УПД файл изготавливается в соответствии с :download:`XSD-схемой <../../xsd/ON_SCHFDOPPR_1_995_01_05_01_05.xsd>`, которой должны удовлетворять документы, согласно приказа ФНС (если не указан параметр documentVersion или указан documentVersion=utd_05_01_05),

-  для УКД файл изготавливается в соответствии с :download:`XSD-схемой <../../xsd/ON_KORSCHFDOPPR_1_996_01_05_01_03.xsd>`, которой должны удовлетворять документы, согласно приказа ФНС (если не указан параметр utd_05_01_05 или указан documentVersion=ucd_05_01_03),

Возможные HTTP-коды возврата:

-  200 (OK) - операция успешно завершена;

-  400 (Bad Request) - данные в запросе имеют неверный формат или отсутствуют обязательные параметры;

-  401 (Unauthorized) - в запросе отсутствует HTTP-заголовок ``Authorization``, или в этом заголовке содержатся некорректные авторизационные данные;

-  403 (Forbidden) - доступ к ящику с предоставленным авторизационным токеном запрещен, либо у пользователя нет доступа к запрашиваемому
   документу;

-  405 (Method not allowed) - используется неподходящий HTTP-метод;

-  500 (Internal server error) - при обработке запроса возникла непредвиденная ошибка.
