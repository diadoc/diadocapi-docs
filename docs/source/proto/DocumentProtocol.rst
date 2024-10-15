DocumentProtocol
================

Структура ``DocumentProtocol`` хранит печатную форму протокола передачи документа и подпись к ней.

.. code-block:: protobuf

    message DocumentProtocol {
        required bytes PrintForm = 1;
        required bytes Signature = 2;
    }

- ``PrintForm`` — содержимое печатной формы в формате PDF.
- ``Signature`` — электронная подпись к печатной форме протокола в формате :rfc:`CMS SignedData <5652#section-5>` в `DER <http://www.itu.int/ITU-T/studygroups/com17/languages/X.690-0207.pdf>`__-кодировке.


----

.. rubric:: См. также

*Структура используется:*
	- в теле ответа метода :doc:`../http/GenerateDocumentProtocol`