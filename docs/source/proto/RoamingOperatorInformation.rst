RoamingOperatorInformation
==========================

Структура содержит информацию о роуминговом операторе и о функциях, которые поддерживает этот оператор.

.. code-block:: protobuf

    message RoamingOperator {
        required string FnsId = 1;
        required string Name = 2;
        required bool IsActive = 3;
        repeated OperatorFeature Features = 4; 
    }
	
    message OperatorFeature {
        required string Name = 1;
        required string Description = 2;
    }
   
- ``FnsId`` — идентификатор оператора, содержит первые три знака ``fnsParticipantId``.
- ``Name`` — наименование оператора.
- ``IsActive`` — признак доступности оператора; имеет значение ``false`` для отключенных операторов и старых ``fnsId``.
- ``Features`` — функция, которую поддерживает оператор, представленная структурой ``OperatorFeature`` с полями:

	- ``Name`` — наименование функции.
	- ``Description`` — описание функции.
	
----

Смотри также
^^^^^^^^^^^^

Структура используется:
	- в теле ответа метода :doc:`../http/GetRoamingOperators`.
