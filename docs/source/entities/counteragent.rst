Контрагент
==========

**Контрагент** — :doc:`ящик <box>`, с которым установлен статус партнерских взаимоотношений в Диадоке.

Ящики, с которыми вы обмениваетесь документами, можно добавить в :doc:`список контрагентов <../Counteragents>`. Для этого нужно отправить приглашение на обмен документами и получить положительный ответ.

Отправить приглашение можно не только организациям, которые работают в Диадоке, но и работающим с другими операторами ЭДО. Такие организации называются роуминговыми контрагентами. Найти список операторов, с которыми Диадок поддерживает роуминг, можно на `сайте <https://www.diadoc.ru/roaming/working-with>`__.

Представление в API
-------------------

В API контрагент представлен структурой :doc:`../proto/Counteragent`.

*Руководства:*
 - :doc:`../Counteragents`

*Методы для работы с контрагентами:*
 - :doc:`../http/GetCounteragents` — осуществляет поиск контрагентов по указанным параметрам.
 - :doc:`../http/GetCounteragent` — возвращает информацию о контрагенте.
 - :doc:`../http/AcquireCounteragent` — отправляет контрагенту приглашение к обмену документами.
 - :doc:`../http/BreakWithCounteragent` — разрывает отношения между контрагентами, а также отзывает или отклоняет приглашение к обмену документами.
 - :doc:`../http/GetCounteragentCertificates` — возвращает сертификаты контрагента.