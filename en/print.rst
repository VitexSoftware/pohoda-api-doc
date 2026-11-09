Printing and attachments
========================

Schema ``print.xsd`` (prefix ``prn``), element ``prn:print``; the answer is
``prn:printResponse`` with ``rdc:printDetails``.

With this request Pohoda prints a report for a record to a printer,
generates a PDF, saves it to a file or sends it by e-mail.

Elements (``print.xsd``, selection)
-----------------------------------

``record``
   the record to print (agenda + ``id``).
``printerSettings``
   ``report`` (report ``id``), ``printer``, ``pdf`` (``fileName``,
   ``binaryData`` – return data in the response), ``parameters``.
``sendMail``
   e-mail sending: ``to``, ``cc``, ``bcc``, ``subject``, ``body``,
   ``attachments``, ``priority``, ``returnReceipt``, ``disposNotif``.
``isdoc``
   export to ISDOC format (also a standalone schema ``isdoc.xsd``).

The response contains ``rdc:attachment`` with ``rdc:idReport`` and Base64
``rdc:data`` (``fileName`` attribute, ``code="base64"``).

.. note::

   Exact required elements are per the ``print.xsd`` of your version. An
   example call is in the Riesenia Pohoda library (``PrintRequest``).

Document attachments
--------------------

Record attachments live in the SQL tables ``DOC`` / ``DocDirs``; in XML they
are created via ``attachments`` elements in documents (e.g.
``stockAttach``).
