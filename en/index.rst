.. image:: _static/pohoda.svg
   :align: center
   :width: 140px
   :alt: Pohoda logo
   :target: https://github.com/VitexSoftware/pohoda-api-doc

Stormware Pohoda Integration Interfaces
========================================

This guide summarizes the ways an external application can talk to the
**Stormware Pohoda** accounting system: data exchange in **XML**
(``dataPack`` / ``responsePack``), the **mServer** HTTP server, and direct
access to the **SQL database**. It is not a description of any particular
client library but of Pohoda's own interfaces, usable from any language.

The content is compiled from the Stormware XSD schemas (namespaces
``http://www.stormware.cz/schema/version_2/*.xsd``), the official
documentation at `stormware.cz/pohoda/xml
<https://www.stormware.cz/pohoda/xml/>`_, and cross-checked against the
VitexSoftware and Spoje.Net client libraries (see
:doc:`client_libraries`). Examples use **XML**, the native format of the
interface.

.. note::

   This is not an official publication of STORMWARE s.r.o. Statements that
   could not be verified against an official source are explicitly marked
   *unverified*.

.. toctree::
   :maxdepth: 2

   introduction
   xml_format
   import_data
   list_request
   responses_errors
   types_and_codes
   agendas
   invoices
   address_book
   stock
   print
   mserver
   sql_database
   client_libraries
