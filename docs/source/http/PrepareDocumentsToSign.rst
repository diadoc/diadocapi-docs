PrepareDocumentsToSign
======================

Метод ``PrepareDocumentsToSign`` подготавливает документы к подписанию.

.. http:post:: /PrepareDocumentsToSign

	:requestheader Authorization: данные, необходимые для :doc:`авторизации <../Authorization>`.

	:request Body: Тело запроса должно содержать структуру :doc:`../proto/PrepareDocumentsToSignRequest`.

	:statuscode 200: операция успешно завершена.
	:statuscode 400: данные в запросе имеют неверный формат.
	:statuscode 401: в запросе отсутствует HTTP-заголовок ``Authorization`` или в этом заголовке содержатся некорректные авторизационные данные.
	:statuscode 402: у организации с указанным идентификатором ``boxId`` закончилась подписка на API.
	:statuscode 403: у пользователя нет доступа к документу или к ящику с предоставленным авторизационным токеном.
	:statuscode 404: не найден ящик с указанным идентификатором или не найден черновкик или документ для патчинга.
	:statuscode 405: используется неподходящий HTTP-метод.
	:statuscode 409: ящик пользователя удален.
	:statuscode 500: при обработке запроса возникла непредвиденная ошибка.

	:response Body: Тело ответа содержит подготовленные к подписанию документы, представленные структурой :doc:`../proto/PrepareDocumentsToSignResponse`. Метод вернет только те документы, которые поддерживают подготовку к подписанию. Проверить возможность подготовки к подписанию можно с помощью свойства ``SupportsContentPatching`` структуры :ref:`DocumentVersionV2` для типа этого документа, полученной методом :doc:`GetDocumentTypes`. Инструкция о получении данных из метода ``GetDocumentTypes`` приведена на странице :doc:`../instructions/getdoctypes`.

Метод не меняет переданное содержимое документа. Он генерирует новое содержимое, помещает его во временное хранилище и возвращает указатель на него в поле ``PrepareDocumentsToSignResponse.DocumentPatchedContents.PatchedContentId``. Этот указатель можно использовать при отправке документа в поле ``PatchedContentId`` в структурах :doc:`../proto/DocumentSignature` и :doc:`../proto/DocumentSenderSignature`.


----

.. rubric:: См. также

*Инструкции:*
	- :doc:`../instructions/preparetosign`
