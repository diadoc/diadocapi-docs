Быстрый старт
=============

Ниже описан простой пример отправки неформализованного документа через систему Диадок из тестовой в тестовую организацию.

Чтобы отправить документ, выполните следующие шаги:

#. Подготовьте две тестовые организации:

	#. Создайте два тестовых ящика с помощью `формы <https://diadoc-widget.kontur.ru/easyregistration/test>`__.
	#. `Добавьте ящики в контрагенты <https://support.kontur.ru/pages/viewpage.action?pageId=83854105>`__ друг к другу с помощью веб-интерфейса Диадока .

#. :doc:`Авторизуйтесь в системе <../Authorization>`, чтобы получить авторизационный токен.

#. Получите идентификатор ящика организации-отправителя с помощью метода :doc:`../http/GetMyOrganizations`.

#. Получите идентификатор ящика организации-контрагента с помощью метода :doc:`../http/GetCounteragents`.

#. Выберите документ на отправку и подпишите его тестовой подписью с помощью флага :doc:`SignedContent.SignWithTestSignature <../proto/SignedContent>`.

#. Отправьте документ с помощью метода :doc:`../http/PostMessage`.

#. Проверьте статус отправленного документа с помощью метода :doc:`../http/GetDocument`.

Пример C#
---------

.. code-block:: csharp

	var crypt = new WinApiCrypt();
	var diadocApi = new DiadocApi(
		clientId,
		apiUrl,
		crypt);

	// Авторизация с помощью логина и пароля
	var authToken = diadocApi.Authenticate(login, password);

	// Получение идентификатора ящика отправителя
	var organizationList = diadocApi.GetMyOrganizations(authToken);
	var organizations = organizationList.Organizations;
	var myOrgBoxIds = organizations.Select(org => org.Boxes.First().BoxId);

	// Получение идентификатора ящика получателя
	string counteragentStatus = null;
	string afterIndexKey = null;
	var counteragentList = diadocApi.GetCounteragents(authToken, myOrgId, counteragentStatus, afterIndexKey);
	var counteragents = counteragentList.Counteragents;
	var myCounteragentOrgBoxIds = counteragents.Select(c => c.Organization.Boxes.First().BoxId);

	// Подготовка и отправка документа

	// Идентификаторы отправителя и получателя
	var messageToPost = new MessageToPost
	{
		FromBoxId = myOrgBoxIds,
		ToBoxId = myCounteragentOrgBoxIds
	};

	// Заполнение содержимого документа
	string NonformalizedDocumentPath = @"<Путь до файла>"; // путь до файла, который нужно отправить
	var content = File.ReadAllBytes(NonformalizedDocumentPath); // бинарное содержимое неформализованного документа

	// Добавление информации о файле в структуру DocumentAttachment
	var documentAttachment = new DocumentAttachment
	{
		TypeNamedId = "nonformalized",
		
		SignedContent = new SignedContent
		{
			Content = content,
			SignWithTestSignature = true
		}

		Comment = "Текстовый комментарий к документу",
		CustomDocumentId = "Строковый идентификатор учетной системы",

		Metadata =
		{
			new MetadataItem
			{
				Key = "FileName",
				Value = Path.GetFileNameWithoutExtension(NonformalizedDocumentPath)
			}
		}
	};

	// Заполнение информации о документе в MessageToPost
	messageToPost.DocumentAttachments.Add(documentAttachment);

	// Отправка документа
	var response = diadocApi.PostMessage(authToken, messageToPost);
	var responseDocument = response.Entities.FirstOrDefault(e => string.IsNullOrEmpty(e.ParentEntityId)); // т.к. у документа нет "родительских сущностей"

	// Проверка статуса
	var document = api.GetDocument(authToken, myOrgBoxIds, response.MessageId, responseDocument.EntityId);
	var status = document.DocflowStatus.PrimaryStatus;
	Console.WriteLine("Сообщение отправлено, статус: " + status);

..