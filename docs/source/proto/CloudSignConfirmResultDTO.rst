CloudSignConfirmResult
======================

.. code-block:: protobuf

        message CloudSignConfirmResult {
            repeated Content_v2 Signatures = 1;
        }
        

Содержит подписи, созданные с использованием CloudCrypt сертификата, в том же количестве и в порядке соответствующим, исходным данным запроса :doc:`CloudSignRequest`.
