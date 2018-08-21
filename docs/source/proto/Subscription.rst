Subscription
============

.. code-block:: protobuf

    message Subscription
    {
        required string Id = 1;
        required bool IsSubscribed = 2;
    }

Структура содержит информацию о том, подписан ли сотрудник на конкретное почтовое уведомление. Содержится в структурах :doc:`EmployeeSubscriptions` и :doc:`SubscriptionsToUpdate`.

 - *Id* - строковой идентификатор уведомления
 - *IsSubscribed* - подписан ли сотрудник
 
.. csv-table:: Почтовые уведомления
   :header: "Идентификатор", "Описание"
   :widths: 2, 10

   "CounteragentInvitation", "О приглашениях от контрагентов"
   "CounteragentInvitationResponses", "Об ответах контрагентов на приглашения"
   "NewIncomingDocuments", "О новых входящих документах"
   "CounteragentSignatures", "О положительном результате подписания документа контрагентом"
   "CounteragentSignatureDenials", "Об отрицательном результате подписания документа контрагентом"
   "ResolutionRequests", "О документах, переданных мне на подпись или согласование"
   "ResolutionResults", "О результате согласования документа"
   "EmployeeRequests", "О запросах доступа от новых пользователей"
   "News", "Новости Диадока и законодательства в области электронных документов"
   "ChatMessages", "Новые сообщения"
