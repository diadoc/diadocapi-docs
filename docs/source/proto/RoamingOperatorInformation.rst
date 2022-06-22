RoamingOperatorInformation
==========================

Структура содержит список всех идентификаторов роуминговых операторов и информацию о функциях, доступных этим операторам.

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
- ``Features`` — функции, доступные оператору, представленые структурой ``OperatorFeature`` с полями:

	- ``Name`` — наименование функции.
	- ``Description`` — описание функции.

----

.. rubric:: Использование

Структура возвращается методом :doc:`../http/GetRoamingOperators`.
