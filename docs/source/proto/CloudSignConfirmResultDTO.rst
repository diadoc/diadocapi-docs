CloudSignConfirmResult
======================

.. code-block:: protobuf

        message CloudSignConfirmResult {
            repeated Content_v2 Signatures = 1;
        }
        

Содержит облачные подписи в том же количестве и порядке, что и соответствующие исходные данные запроса :doc:`CloudSignRequest`.
