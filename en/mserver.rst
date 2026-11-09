mServer: the HTTP interface
===========================

**POHODA mServer** is an HTTP server built into Pohoda. It accepts a
``dataPack`` in the body of an HTTP POST and returns a ``responsePack`` –
the same XML as file import/export (:doc:`xml_format`).

Operation
---------

* Pohoda must be running; **one mServer configuration occupies one program
  instance**, which cannot be used for manual work at the same time. Start
  Pohoda a second time for manual work.
* Typical use: mKasa, third-party applications, web shops.
* Stormware recommends a server OS **on an internal network**; do not run
  mServer on a machine with a public IP address. Traffic is plain HTTP by
  default (older documentation) – put TLS on a reverse proxy if needed.

Source: `stormware.cz/pohoda/xml/mserver
<https://www.stormware.cz/pohoda/xml/mserver/>`_ (overview); the details
below follow the implementation of the PHP-Pohoda-Connector client.

Endpoints
---------

.. list-table::
   :header-rows: 1
   :widths: 22 78

   * - Path
     - Use
   * - ``/xml``
     - POST with a ``dataPack`` (import and export). The path must be
       present, otherwise the server returns ``404``. Example:
       ``http://192.168.0.1:444/xml``.
   * - ``/status``
     - Availability check (POST with authentication). The response contains
       the text ``Response from POHODA mServer`` (used by ``isOnline()`` in
       PHP-Pohoda-Connector). *Unverified* in official documentation.

HTTP headers
------------

.. list-table::
   :header-rows: 1
   :widths: 28 72

   * - Header
     - Meaning
   * - ``STW-Authorization``
     - ``Basic <base64(user:password)>`` – a Pohoda user. Required.
   * - ``STW-Application``
     - Application name (shown in the XML Import agenda).
   * - ``STW-Instance``
     - Selects a specific mServer instance / configuration.
   * - ``STW-Check-Duplicity``
     - ``true`` – enables duplicate checking by package ``id``.
   * - ``Content-Type`` / ``Accept``
     - ``application/xml``

Example with curl:

.. code-block:: bash

   curl -sS -X POST http://192.168.0.1:444/xml \
     -H "STW-Authorization: Basic $(printf 'user:pass' | base64)" \
     -H "STW-Application: MyApp" \
     -H "Content-Type: application/xml" \
     --data-binary @datapack.xml

.. note::

   The ASP/HTTP connector for mServer (official Stormware guide) uses the
   header ``Stw-Server-Name`` to select a server; do not use it in direct
   calls.

Response codes
--------------

.. list-table::
   :header-rows: 1
   :widths: 12 88

   * - Code
     - Typical cause with mServer
   * - ``200``
     - Request processed; the per-record state is in the XML response.
   * - ``400``
     - Syntactically invalid request (bad XML).
   * - ``401``
     - Missing authentication, or the user does not exist in Pohoda.
   * - ``403``
     - The user may not open the accounting unit.
   * - ``404``
     - Wrong URL – the ``/xml`` path is missing.
   * - ``405``
     - A method other than POST was used.
   * - ``408``
     - Processing time exceeded.
   * - ``500``
     - Unspecified processing error.
   * - ``502`` / ``503`` / ``504``
     - Proxy / service unavailable / gateway timeout.

Notes for clients
-----------------

* The response is Windows-1250 – convert to UTF-8.
* Set a sensible timeout (PHP-Pohoda-Connector defaults to 30 s); large
  exports take longer.
* Compression is optional (``POHODA_COMPRESS``).
