.. image:: _static/pohoda.svg
   :align: center
   :width: 140px
   :alt: Logo Pohoda
   :target: https://github.com/VitexSoftware/pohoda-api-doc

Integrační rozhraní Stormware Pohoda
=====================================

Tento průvodce shrnuje způsoby, jak se z externích aplikací propojit s
účetním systémem **Stormware Pohoda**: výměnu dat v **XML** (``dataPack`` /
``responsePack``), HTTP server **mServer** a přímý přístup do **SQL
databáze**. Nejde o popis konkrétní klientské knihovny, ale o samotná
rozhraní Pohody, použitelná z libovolného jazyka.

Obsah je sestaven z XSD schémat Stormware (jmenné prostory
``http://www.stormware.cz/schema/version_2/*.xsd``), z oficiální dokumentace
na `stormware.cz/pohoda/xml <https://www.stormware.cz/pohoda/xml/>`_ a ověřen
proti klientským knihovnám VitexSoftware a Spoje.Net (viz
:doc:`klientske_knihovny`). Příklady jsou v **XML**, protože to je nativní
formát rozhraní.

.. note::

   Dokumentace není oficiální publikací společnosti STORMWARE s.r.o.
   Místa, která se nepodařilo ověřit proti oficiálnímu zdroji, jsou
   v textu výslovně označena jako *neověřeno*.

.. toctree::
   :maxdepth: 2

   uvod
   xml_format
   import_dat
   list_request
   odpovedi_chyby
   typy_a_ciselniky
   agendy
   faktury
   adresar
   sklady
   tisk
   mserver
   sql_databaze
   klientske_knihovny
