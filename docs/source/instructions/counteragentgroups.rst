Группы контрагентов
===================

.. contents:: :local:

Контрагентов, с которыми установлены партнерские отношения, можно распределять по группам.

По умолчанию все контрагенты в группе могут отправлять документы в любое подразделение организации. Но вы можете указать для каждой группы контрагентов подразделения, в которые смогут отправлять документы контрагенты из этой группы. Это может быть полезно в случае, если разные подразделения организации работают с документами от разных контрагентов.


Создание группы контрагентов
----------------------------

Чтобы создать группу контрагентов, выполните следующие действия:

	#. С помощью метода :doc:`../http/CreateCounteragentGroup` создайте группу и укажите, в какие подразделения контрагенты группы смогут отправлять документы. В ответе метод вернет информацию о созданной группе.
	#. С помощью метода :doc:`../http/AddCounteragentToGroup` добавьте контрагентов в созданную группу. Вызвать метод нужно для каждого контрагента, которого вы хотите добавить в группу.

**Пример HTTP-запроса метода CreateCounteragentGroup:**

.. literalinclude:: ../include/сreateCounteragentGroup_query.txt

**Пример тела запроса метода CreateCounteragentGroup:**

.. literalinclude:: ../include/сreateCounteragentGroup_body.txt
	:language: json

**Пример ответа метода CreateCounteragentGroup:**

.. literalinclude:: ../include/сreateCounteragentGroup_resp.txt
	:language: json

**Пример HTTP-запроса метода AddCounteragentToGroup:**

.. literalinclude:: ../include/addCounteragentToGroup_query.txt


Получение списка групп контрагентов
-----------------------------------

Чтобы отредактировать, удалить или получить информацию о конкретной группе, нужно знать ее идентификатор. Получить идентификаторы и информацию обо всех группах организации можно с помощью метода :doc:`../http/GetCounteragentGroups`. Метод возвращает список всех существующих групп в указанной организации, включая группу по умолчанию.

**Пример HTTP-запроса метода GetCounteragentGroups:**

.. literalinclude:: ../include/getCounteragentGroups_query.txt

**Пример ответа метода GetCounteragentGroups:**

.. container:: toggle

	.. literalinclude:: ../include/getCounteragentGroups_resp.txt
		:language: json


Получение информации о группе контрагентов
------------------------------------------

Чтобы получить информацию о группе контрагентов по ее идентификатору, используйте метод :doc:`../http/GetCounteragentGroup`.

**Пример HTTP-запроса метода GetCounteragentGroup:**

.. literalinclude:: ../include/getCounteragentGroup_query.txt

**Пример тела ответа метода GetCounteragentGroup:**

.. literalinclude:: ../include/getCounteragentGroup_resp.txt
	:language: json


Получение списка контрагентов группы
------------------------------------

Чтобы получить информацию о контрагентах, состоящих в группе, используйте метод :doc:`../http/GetCounteragentsFromGroup`. По идентификатору группы он вернет список контрагентов этой группы.

**Пример HTTP-запроса метода GetCounteragentsFromGroup:**

.. literalinclude:: ../include/getCounteragentsFromGroup_query.txt

**Пример тела ответа метода GetCounteragentsFromGroup:**

.. literalinclude:: ../include/getCounteragentsFromGroup_resp.txt
	:language: json


Редактирование группы контрагентов
----------------------------------

Чтобы изменить название или список подразделений, в которые контрагенты группы могут отправлять документы, используйте метод :doc:`../http/UpdateCounteragentGroup`. На странице метода описаны все случаи редактирования подразделений группы.

**Пример HTTP-запроса метода UpdateCounteragentGroup:**

.. literalinclude:: ../include/updateCounteragentGroup_query.txt

**Пример тела запроса метода UpdateCounteragentGroup:**

.. literalinclude:: ../include/updateCounteragentGroup_newstruct_body.txt
	:language: json

**Пример тела ответа метода UpdateCounteragentGroup:**

.. literalinclude:: ../include/updateCounteragentGroup_newstruct_resp.txt
	:language: json


Удаление группы контрагентов
----------------------------

Чтобы удалить группу контрагентов, используйте метод :doc:`../http/DeleteCounteragentGroup`. После удаления группы все контрагенты, находящиеся в ней, будут перемещены в группу «По умолчанию».

**Пример HTTP-запроса метода DeleteCounteragentGroup:**

.. literalinclude:: ../include/deleteCounteragentGroup_query.txt


----

.. rubric:: См. также

*Определение:*
	- :doc:`../entities/counteragent`

.. include:: ../include/seealso_instr_counteragentgroup.txt