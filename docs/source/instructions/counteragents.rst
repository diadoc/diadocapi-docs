Работа с контрагентами
======================

.. contents:: :local:

Список активных контрагентов
----------------------------

У каждой организации в Диадоке есть список активных :doc:`контрагентов <../entities/counteragent>` — организаций, с которыми установлен статус партнерских взаимоотношений.

Веб-интерфейс Диадока отображает список активных контрагентов, чтобы упростить пользователю выбор контрагента в диалогах. Вы можете реализовать подобную функциональность в вашем интеграционном решении и получить такой же список. Сделать это можно с помощью метода :doc:`../http/GetCounteragents`.

Изменить содержимое списка можно следующими методами:

- :doc:`../http/AcquireCounteragent` — добавляет контрагента в список активных;
- :doc:`../http/BreakWithCounteragent` — удаляет контрагента из списка активных.

Управлять списком активных контрагентов можно и через `веб-интерфейс Диадока <https://diadoc.kontur.ru>`__. Изменения, внесенные через веб-интерфейс, отражаются на списках контрагентов, полученных через API, и наоборот. Поэтому в некоторых случаях проще не реализовывать логику управления списком активных контрагентов в интеграционном решении и выполнять такое управление через веб-интерфейс. Список контрагентов можно сформировать через веб-интерфейс перед вводом интеграционного решения в эксплуатацию. Это может быть удобно в случаях, когда списки контрагентов организаций-потребителей интеграционного решения небольшие и редко изменяются.

Обмениваться документами можно с любыми организациями — даже с теми, которые не находятся в списке активных контрагентов. Исключение составляют следующие организации:

	- Организации, установившие в своих реквизитах настройку «Документы от контрагентов» в значение «Только организации из списка "Ваши контрагенты"». В этом случае отправить документ такой организации может только организация из списка ее активных контрагентов.
	- Организации, работающие с другими операторами ЭДО.

Получение информации о контрагенте
----------------------------------

Получить подробную информацию о контрагенте и статусе партнерства с ним можно по идентификатору организации-контрагента. Для этого используйте метод :doc:`../http/GetCounteragent`.

Получить ленту событий по изменению отношений с контрагентами можно с помощью метода :doc:`../http/GetCounteragentEvents`.

Поиск контрагентов
------------------

Осуществлять поиск контрагентов можно с помощью следующих методов:

- :doc:`../http/GetOrganizationsByInnKpp` — возвращает организации с указанными ИНН и КПП.
- :doc:`../http/GetOrganizationsByInnList` — возвращает организации и их статусы по указанному списку ИНН.
- :doc:`../http/GetBox` — по идентификатору ящика возвращает информацию об организации, которой он принадлежит.
- :doc:`../http/GetOrganization` — по идентификатору организации возвращает принадлежащий ей ящик и ее данные: например, ИНН, КПП, название и т.п.