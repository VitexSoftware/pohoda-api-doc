SQL databáze Pohody
===================

Pohoda (edice SQL a E1) ukládá data do Microsoft SQL Serveru. Název databáze
má tvar ``StwPh_<IČO>_<rok>`` (např. ``StwPh_12345678_2026`` – jedna
databáze na účetní jednotku a rok). Přístup: ODBC / ``sqlsrv``, port 1433.

.. warning::

   Přímý **zápis** do tabulek obchází kontroly Pohody (číselné řady, DPH,
   saldo, vazby) a může poškodit data. Pro zápis používejte
   :doc:`import_dat`. Čtení je bezpečné, nejlépe pod účtem pouze
   s právem ``SELECT``. Schéma se mezi verzemi Pohody mění.

Pojmenování tabulek
-------------------

Tabulky mají krátké kódy agend (české zkratky); položky dokladů mají
příponu ``pol``, číselníky předponu ``s``, předkontace ``pPK``:

.. list-table::
   :header-rows: 1
   :widths: 15 28 57

   * - Tabulka
     - Třída v php-spojenet-pohoda-sql
     - Obsah
   * - ``AD``
     - ``Adresar``
     - adresář
   * - ``FA`` / ``FApol``
     - ``Faktura`` / ``FakturaPolozka``
     - vydané a přijaté faktury a jejich položky
   * - ``OBJ`` / ``OBJpol``
     - ``ObjednavkaPrijata``
     - přijaté objednávky
   * - ``NAB`` / ``NABpol``
     - ``Nabidka``
     - nabídky
   * - ``BV`` / ``BVpol``
     - ``BankovniVypis``
     - bankovní výpisy
   * - ``PH`` / ``PHpol``
     - ``Pokladna``
     - pokladna
   * - ``HO`` / ``HOpol``
     - ``HotovostniOperace``
     - hotovostní operace
   * - ``IM``, ``IMpohyb``, ``IModpis``
     - ``Majetek`` ...
     - majetek, pohyby, odpisy
   * - ``ZAM``
     - ``Zamestnanec``
     - zaměstnanci
   * - ``Uhrady``
     - ``Uhrada``
     - úhrady
   * - ``sCRady``
     - ``CiselnaRada``
     - číselné řady
   * - ``pPK``
     - ``Predkontace``
     - předkontace
   * - ``DOC``
     - ``DOC``
     - přílohy dokladů

Projekt ``php-spojenet-pohoda-sql`` obsahuje 443 šablon tabulek
(``templates/``) a tříd pro nejčastější z nich (``src/``). Prefix ``Lg``
označuje logovací tabulky (např. ``LgFA``).

Běžné sloupce
-------------

Většina tabulek obsahuje ``ID`` (primární klíč), ``UsrOrder``, vazby
``Ref*`` / ``Rel*`` na číselníky (např. ``RefCin`` – činnost, ``RefStr`` –
středisko, ``RefUcet`` – účet), a časové značky ``DatCreate`` a
``DatSave``. ``DatSave`` lze použít pro **inkrementální čtení změn** (dotaz
na záznamy změněné od určité chvíle).

Připojení
---------

.. code-block:: ini

   DB_TYPE=sqlsrv
   DB_HOST=sql.example.org
   DB_PORT=1433
   DB_DATABASE=StwPh_12345678_2026
   DB_USERNAME=pohoda_ro
   DB_PASSWORD=***
   DB_SETTINGS=encrypt=false

Tyto proměnné používá knihovna php-spojenet-pohoda-sql (viz
:doc:`klientske_knihovny`).
