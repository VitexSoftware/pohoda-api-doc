The Pohoda SQL database
=======================

Pohoda (SQL and E1 editions) stores data in Microsoft SQL Server. The database
is named ``StwPh_<IČO>_<year>`` (e.g. ``StwPh_12345678_2026`` – one database
per accounting unit and year). Access via ODBC / ``sqlsrv``, port 1433.

.. warning::

   Direct **writes** to tables bypass Pohoda's checks (number series, VAT,
   balances, links) and may corrupt data. Use :doc:`import_data` for writing.
   Reading is safe, ideally under an account with ``SELECT`` rights only. The
   schema changes between Pohoda versions.

Table naming
------------

Tables use short agenda codes (Czech abbreviations); document items carry the
suffix ``pol``, code lists the prefix ``s``, pre-accountings ``pPK``:

.. list-table::
   :header-rows: 1
   :widths: 15 28 57

   * - Table
     - Class in php-spojenet-pohoda-sql
     - Content
   * - ``AD``
     - ``Adresar``
     - address book
   * - ``FA`` / ``FApol``
     - ``Faktura`` / ``FakturaPolozka``
     - issued and received invoices and their items
   * - ``OBJ`` / ``OBJpol``
     - ``ObjednavkaPrijata``
     - received orders
   * - ``NAB`` / ``NABpol``
     - ``Nabidka``
     - offers
   * - ``BV`` / ``BVpol``
     - ``BankovniVypis``
     - bank statements
   * - ``PH`` / ``PHpol``
     - ``Pokladna``
     - cash register
   * - ``HO`` / ``HOpol``
     - ``HotovostniOperace``
     - cash operations
   * - ``IM``, ``IMpohyb``, ``IModpis``
     - ``Majetek`` ...
     - assets, movements, depreciation
   * - ``ZAM``
     - ``Zamestnanec``
     - employees
   * - ``Uhrady``
     - ``Uhrada``
     - payments
   * - ``sCRady``
     - ``CiselnaRada``
     - number series
   * - ``pPK``
     - ``Predkontace``
     - pre-accountings
   * - ``DOC``
     - ``DOC``
     - document attachments

The ``php-spojenet-pohoda-sql`` project contains 443 table templates
(``templates/``) and classes for the most common ones (``src/``). The prefix
``Lg`` denotes log tables (e.g. ``LgFA``).

Common columns
--------------

Most tables contain ``ID`` (primary key), ``UsrOrder``, ``Ref*`` / ``Rel*``
links to code lists (e.g. ``RefCin`` – activity, ``RefStr`` – centre,
``RefUcet`` – account), and the timestamps ``DatCreate`` and ``DatSave``.
``DatSave`` can drive **incremental change reading** (query records changed
since a given moment).

Connection
----------

.. code-block:: ini

   DB_TYPE=sqlsrv
   DB_HOST=sql.example.org
   DB_PORT=1433
   DB_DATABASE=StwPh_12345678_2026
   DB_USERNAME=pohoda_ro
   DB_PASSWORD=***
   DB_SETTINGS=encrypt=false

These variables are used by the php-spojenet-pohoda-sql library (see
:doc:`client_libraries`).
