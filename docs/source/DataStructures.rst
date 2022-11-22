Передача данных в API
=====================

Для сериализации и десериализации структур данных, передаваемых в запросах и ответах API Диадока, используются следующие форматы:

- `Google Protocol Buffers <https://developers.google.com/protocol-buffers/>`__,
- `JSON <http://json.org/json-ru.html>`__.

По умолчанию структуры передаются и возвращаются в формате Protocol Buffers.
Мы рекомендуем использовать в интеграционных решениях именно этот формат. Его основное преимущество по сравнению с форматом JSON — это обратная совместимость: в JSON поддерживаются только последние версии структур данных.

Перед выбором формата данных для своего интеграционного решения ознакомьтесь со `статьей о сравнении этих форматов <http://blog.codeclimate.com/blog/2014/06/05/choose-protocol-buffers/>`__ или другими ресурсами.

По умолчанию состав данных, с которыми работают методы API Диадока, для всех форматах одинаков, если не сказано обратное.

Google Protocol Buffers
-----------------------

Синтаксис языка Protocol Buffers описан `здесь <https://developers.google.com/protocol-buffers/docs/proto>`__.

Для различных платформ и языков программирования существуют готовые библиотеки для сериализации и десериализации данных в формат Protocol Buffers. Например:

- для языков C++, Java, Python — `официальная реализация Google <https://github.com/google/protobuf>`__;
- для платформы Microsoft® .NET — `проект protobuf-net <https://code.google.com/p/protobuf-net/>`__;
- `другие решения <https://github.com/protocolbuffers/protobuf/blob/main/docs/third_party.md>`__.

`SDK Диадока <https://diadoc.kontur.ru/sdk/>`__ уже содержит все необходимые библиотеки для сериализации и десериализации данных в формат Protocol Buffers.

JSON
----

Чтобы работать с данными в формате JSON, передайте в HTTP запросах к API Диадока следующие заголовки:

- ``Content-Type: application/json; charset=utf-8`` — чтобы передать данные в формате JSON в теле запроса,
- ``Accept: application/json`` — чтобы получить данные в формате JSON в теле ответа.
  
Бинарное содержимое передавайте с помощью :rfc:`base64<4648#section-4>`-строк.

Пример представления данных
---------------------------

Структура :doc:`proto/SearchDocflowsRequest` в разных форматах будет выглядеть следующим образом:

- в формате Protocol Buffers:

 .. code-block:: protobuf

    message SearchDocflowsRequest
    {
        required string QueryString = 1;
        optional int32 Count = 2 [default = 100];
        optional int32 FirstIndex = 3;
        optional SearchScope Scope = 4 [default = SearchScopeAny];
        optional bool InjectEntityContent = 5 [default = false];
    }

    enum SearchScope
    {
        SearchScopeAny = 0;
        SearchScopeIncoming = 1;
        SearchScopeOutgoing = 2;
        SearchScopeDeleted = 3;
        SearchScopeInternal = 4;
    }

- в формате JSON:

 .. code-block:: json

    {  
        "QueryString": "example",
        "Count": 100,
        "FirstIndex": 1,
        "Scope": 0,
        "InjectEntityContent": false
    }