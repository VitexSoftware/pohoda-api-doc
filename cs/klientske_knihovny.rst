Klientské knihovny a nástroje
=============================

Tato dokumentace byla ověřována proti čtyřem projektům:

.. list-table::
   :header-rows: 1
   :widths: 30 70

   * - Projekt
     - Popis
   * - `riesenia/pohoda <https://github.com/riesenia/pohoda>`_
       (``php-pohoda-xml``)
     - Generátor ``dataPack`` XML v PHP (importy faktur, objednávek,
       skladu...); spec soubory jsou dobrou zásobárnou příkladů.
   * - `php-vitexsoftware-pohoda-connector
       <https://github.com/VitexSoftware/PHP-Pohoda-Connector>`_
     - Klient mServeru (``mServer\Client``), zpracování odpovědí
       (70+ typů), proměnné ``POHODA_ICO``, ``POHODA_URL``,
       ``POHODA_USERNAME``, ``POHODA_PASSWORD``, ``POHODA_TIMEOUT``,
       ``POHODA_COMPRESS``, ``POHODA_DEBUG``.
   * - `php-vitexsoftware-pohodaser
       <https://github.com/VitexSoftware/php-vitexsoftware-pohodaser>`_
     - Serializace/deserializace XML podle XSD (JMS Serializer,
       goetas xsd2php); obsahuje kopii XSD schémat Stormware.
   * - `php-spojenet-pohoda-sql
       <https://github.com/Spoje-NET/PohodaSQL>`_
     - Čtení z SQL databáze Pohody (``sqlsrv``), definice tabulek
       a ``idAgend``.

Oficiální zdroje
----------------

* `stormware.cz/pohoda/xml <https://www.stormware.cz/pohoda/xml/>`_
  – XML rozhraní, schémata ke stažení.
* `stormware.cz/pohoda/xml/mserver
  <https://www.stormware.cz/pohoda/xml/mserver/>`_ – mServer.
