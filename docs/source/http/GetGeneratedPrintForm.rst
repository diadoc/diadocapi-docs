GetGeneratedPrintForm
=====================

Имя ресурса: **/GetGeneratedPrintForm**

HTTP-метод: **GET**

Параметры строки запроса:

-  *printFormId* - идентификатор печатной формы, полученный с помощью методов :doc:`GeneratePrintForm` или :doc:`GeneratePrintFormFromAttachment`.

В запросе должен присутствовать HTTP-заголовок ``Authorization`` с необходимыми данными для :doc:`авторизации <../Authorization>`.

Если печатная форма еще не построена, ответ будет содержать HTTP-заголовок ``Retry-After`` с примерной оценкой времени (в секундах), оставшегося до завершения.

Клиент может повторить вызов :doc:`GetGeneratedPrintForm` через указанное время.