Introduction and integration options
====================================

Pohoda offers three basic ways to exchange data:

.. list-table::
   :header-rows: 1
   :widths: 18 42 40

   * - Route
     - Principle
     - Best for
   * - **XML file**
     - A ``dataPack`` file is imported / exported in the *File → Data
       communication → XML import/export* agenda or from the command line.
     - Batch transfers, manual exchange with an accountant.
   * - **mServer**
     - Pohoda running in HTTP server mode accepts the same XML over HTTP
       POST (:doc:`mserver`).
     - Web shops, cash registers, real-time integration.
   * - **SQL database**
     - Direct access to the Microsoft SQL Server database
       (:doc:`sql_database`).
     - Reports and reading. Writing is discouraged.

Rule of thumb: **write through XML/mServer, read from SQL if you like.**
Writing straight into tables bypasses the checks, number series and
recalculations Pohoda performs.

Basic concepts
--------------

*Agenda*
   A register for one kind of document or record (invoices, orders, address
   book, stock, bank...). See :doc:`agendas`.

*Accounting unit and period*
   Data belongs to a specific company (IČO) and accounting period. A
   ``dataPack`` is therefore marked with ``ico`` (or ``key``) and optionally
   ``period``.

*Schema versions*
   All namespaces are ``version_2``; individual agendas have their own
   ``version`` attribute (typically ``2.0``). Stormware adds new features to
   existing schema versions in a backward-compatible way.

Sources
-------

* XSD schemas – the authoritative description of all elements (``xsd/``
  directory of the php-vitexsoftware-pohodaser project).
* `stormware.cz/pohoda/xml <https://www.stormware.cz/pohoda/xml/>`_ –
  official documentation of the XML interface and mServer.
