PowerOfAttorneyPermissionsInfo
==============================

Структура ``PowerOfAttorneyPermissionsInfo`` хранит информацию о полномочиях из машиночитаемой доверенности.

.. code-block:: protobuf

    message PowerOfAttorneyPermissionsInfo {
        repeated PowerOfAttorneyPermissions Permissions = 1;
        optional string TransferPermissionLoss = 2;
        required string JointPermissions = 3;
    }

    message PowerOfAttorneyPermissions {
        required string Type = 1;
        optional string TextPermission = 2;
        repeated PowerOfAttorneyMachineReadablePermission MachineReadablePermission = 3;
    }

    message PowerOfAttorneyMachineReadablePermission {
        optional string Mnemonic = 1;
        required string Code = 2;
        required string Name = 3;
        repeated PowerOfAttorneyRestrictions Restrictions = 4;
    }

    message PowerOfAttorneyRestrictions {
        required int Id = 1;
        required string Code = 2;
        required string Name = 3;
        optional string ValueName = 4;
        optional string ValueCode = 5;
        optional string ValueText = 6; 
    }

- ``Permissions`` — список обязательных полномочий. Каждый элемент в списке представлен структурой ``PowerOfAttorneyPermissions`` с полями:

	- ``Type`` — тип полномочия. Может принимать значения:

		- ``text`` — текстовое полномочие,
		- ``machineReadable`` — машиночитаемое полномочие.

	- ``TextPermission`` — текстовое содержание полномочия.
	- ``MachineReadablePermission`` — список машиночитаемых полномочий. Каждый элемент списка представлен структурой ``PowerOfAttorneyMachineReadablePermission`` с полями:

		- ``Mnemonic`` — мнемоника полномочия.
		- ``Code`` — код полномочия.
		- ``Name`` — наименование полномочия.
		- ``Restrictions`` — список ограничений к полномочию. Каждый элемент списка представлен структурой ``PowerOfAttorneyRestrictions`` с полями:

			- ``Id`` — порядковый номер ограничения.
			- ``Code`` — код ограничения.
			- ``Name`` — наименование ограничения.
			- ``ValueName`` — наименование значения для ограничения.
			- ``ValueCode`` — код значения для ограничения.
			- ``ValueText`` — текстовое значение для ограничения.

- ``TransferPermissionLoss`` — признак утраты полномочий при передоверии. Может принимать значения:

	- ``notLossOnTransfer`` — полномочия не утрачиваются при передоверии,
	- ``lossOnTransfer`` — полномочия утрачиваются при передоверии.

- ``JointPermissions`` — признак совместного осуществления полномочий. Обеспечивает совместные полномочия в случае, если в доверенности указано несколько представителей. Может принимать значения:

	- ``personal`` — индивидуальные полномочия,
	- ``group`` — совместные полномочия.

----

.. rubric:: См. также

*Структура используется:*
	- в структуре :doc:`PowerOfAttorney`

*Инструкции:*
	- :doc:`/instructions/powerofattorney`