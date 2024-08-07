ParseInvoiceXml
===============

.. warning::
	Метод устарел. Для парсинга документов используйте метод :doc:`../ParseTitleXml`.

Имя ресурса: **/ParseInvoiceXml**

HTTP метод: **POST**

В теле запроса должен содержаться XML-файл СФ/ИСФ.

Файл СФ/ИСФ изготавливается в соответствии с :download:`XML-схемой v5.02 <../../xsd/ON_SFAKT_1_897_01_05_02_02.xsd>` или :download:`XML-схемой v5.01 <../../xsd/ON_SFAKT_1_897_01_05_01_02.xsd>`, котором должны удовлетворять XML-счета-фактуры, согласно приказу ФНС.

В теле ответа содержится сериализованная структура :doc:`../../proto/obsolete/InvoiceInfo`, построенная на основании данных запроса.

Если в теле запроса содержится XML-файл, соответствующий :download:`XML-схеме,v5.02 <../../xsd/ON_SFAKT_1_897_01_05_02_02.xsd>`, то в теле ответа содержится сериализованная структура :doc:`../../proto/obsolete/InvoiceInfo`, с заполненными полями v5.02.

Если в теле запроса содержится XML-файл, соответствующий :download:`XML-схеме, v5.01 <../../xsd/ON_SFAKT_1_897_01_05_01_02.xsd>`, то в теле ответа содержится сериализованная структура :doc:`../../proto/obsolete/InvoiceInfo`, с заполненными полями v5.01.

Возможные HTTP-коды возврата:

-  200 (OK) - операция успешно завершена;

-  400 (Bad Request) - данные в запросе имеют неверный формат или отсутствуют обязательные параметры;

-  405 (Method not allowed) - используется неподходящий HTTP-метод;

-  500 (Internal server error) - при обработке запроса возникла непредвиденная ошибка.
