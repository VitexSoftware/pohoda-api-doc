Úvod a způsoby integrace
========================

Pohoda nabízí tři základní cesty, jak s ní vyměňovat data:

.. list-table::
   :header-rows: 1
   :widths: 18 42 40

   * - Cesta
     - Princip
     - Vhodné pro
   * - **XML soubor**
     - Soubor ``dataPack`` se importuje / exportuje v agendě *Soubor → Datová
       komunikace → XML import/export* nebo z příkazové řádky.
     - Dávkové přenosy, ruční výměna s účetní.
   * - **mServer**
     - Pohoda spuštěná v režimu HTTP serveru přijímá stejné XML přes HTTP
       POST (:doc:`mserver`).
     - Online obchody, pokladny, integrace v reálném čase.
   * - **SQL databáze**
     - Přímý přístup do databáze Microsoft SQL Server (:doc:`sql_databaze`).
     - Reporty a čtení. Zápis se nedoporučuje.

Doporučené pravidlo: **zapisujte přes XML/mServer, čtěte klidně i z SQL.**
Zápis přímo do tabulek obchází kontroly, číselné řady a přepočty, které
Pohoda provádí.

Základní pojmy
--------------

*Agenda*
   Evidence jednoho druhu dokladů či záznamů (faktury, objednávky, adresář,
   sklady, banka...). Viz :doc:`agendy`.

*Účetní jednotka a období*
   Data patří konkrétní firmě (IČO) a účetnímu období. ``dataPack`` je
   proto označen atributy ``ico`` (případně ``key``) a volitelně ``period``.

*Verze schémat*
   Každý jmenný prostor má ``version_2``; konkrétní agendy mají vlastní
   atribut ``version`` (typicky ``2.0``). Nové funkce Stormware přidává
   do stávajících verzí schémat a mění je zpětně kompatibilně.

Zdroje
------

* XSD schémata – autoritativní popis všech elementů (adresář ``xsd/`` v
  projektu php-vitexsoftware-pohodaser).
* `stormware.cz/pohoda/xml <https://www.stormware.cz/pohoda/xml/>`_ –
  oficiální dokumentace XML rozhraní a mServeru.
