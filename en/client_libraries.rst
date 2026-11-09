Client libraries and tools
==========================

This documentation was cross-checked against four projects:

.. list-table::
   :header-rows: 1
   :widths: 30 70

   * - Project
     - Description
   * - `riesenia/pohoda <https://github.com/riesenia/pohoda>`_
       (``php-pohoda-xml``)
     - ``dataPack`` XML generator in PHP (invoice, order, stock imports...);
       the spec files are a good source of examples.
   * - `php-vitexsoftware-pohoda-connector
       <https://github.com/VitexSoftware/PHP-Pohoda-Connector>`_
     - mServer client (``mServer\Client``), response processing (70+ types),
       variables ``POHODA_ICO``, ``POHODA_URL``, ``POHODA_USERNAME``,
       ``POHODA_PASSWORD``, ``POHODA_TIMEOUT``, ``POHODA_COMPRESS``,
       ``POHODA_DEBUG``.
   * - `php-vitexsoftware-pohodaser
       <https://github.com/VitexSoftware/php-vitexsoftware-pohodaser>`_
     - XML serialization/deserialization from the XSD (JMS Serializer, goetas
       xsd2php); ships a copy of the Stormware XSD schemas.
   * - `php-spojenet-pohoda-sql
       <https://github.com/Spoje-NET/PohodaSQL>`_
     - Reading the Pohoda SQL database (``sqlsrv``), table definitions and
       ``idAgend``.

Official sources
----------------

* `stormware.cz/pohoda/xml <https://www.stormware.cz/pohoda/xml/>`_ – XML
  interface, schemas for download.
* `stormware.cz/pohoda/xml/mserver
  <https://www.stormware.cz/pohoda/xml/mserver/>`_ – mServer.
