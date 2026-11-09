Formát XML: dataPack
====================

Veškerá komunikace s Pohodou je výměna dvojic **dataPack → responsePack**.

Kořenový element
----------------

.. code-block:: xml

   <?xml version="1.0" encoding="Windows-1250"?>
   <dat:dataPack
       xmlns:dat="http://www.stormware.cz/schema/version_2/data.xsd"
       xmlns:inv="http://www.stormware.cz/schema/version_2/invoice.xsd"
       xmlns:typ="http://www.stormware.cz/schema/version_2/type.xsd"
       version="2.0" id="import-0001" ico="12345678"
       application="MojeAplikace" note="Import faktur">
     <dat:dataPackItem version="2.0" id="FA-0001">
       <!-- právě jeden element agendy -->
     </dat:dataPackItem>
   </dat:dataPack>

Atributy ``dataPack`` (dle ``data.xsd``)
----------------------------------------

.. list-table::
   :header-rows: 1
   :widths: 20 12 68

   * - Atribut
     - Povinný
     - Význam
   * - ``version``
     - ano
     - Verze balíku. Přípustné: ``1.0``, ``1.1``, ``1.2``, ``2.0``.
   * - ``id``
     - ano
     - Identifikátor balíku (max. 64 znaků). Spolu s ``id`` položky slouží
       ke kontrole duplicit importu.
   * - ``ico``
     - ne
     - IČO firmy, pro kterou je XML určeno; musí souhlasit s IČO účetní
       jednotky. Má přednost před ``key``.
   * - ``key``
     - ne
     - Jedinečný klíč účetnictví, použije se, není-li ``ico``.
   * - ``period``
     - ne
     - Účetní období. Není-li uvedeno, použije se aktuální období
       přihlášeného uživatele; je-li uvedeno a neodpovídá, komunikace
       skončí chybou.
   * - ``application``
     - ano
     - Text zobrazený v poli *Aplikace* v agendě XML Import.
   * - ``note``
     - ano
     - Poznámka zobrazená v záložce *Poznámky* agendy XML Import.
   * - ``programVersion``
     - ne
     - Informativní verze programu.

Každý ``dataPackItem`` má povinné ``version`` (``1.0`` nebo ``2.0``) a
``id`` (max. 64 znaků, unikátní v rámci balíku) a obsahuje **právě jeden**
element agendy (``xsd:any``, tedy bez kontroly obsahu na úrovni obálky).

Nepovinný element ``<dat:transformation>`` (od ``dataPack`` 1.1) umožňuje
nastavit XSL transformaci vstupu (``input``) a výstupu (``output``).

Kódování
--------

Pohoda vždy vytváří XML v kódování **Windows-1250**. Vstup může mít i jiné
kódování, pokud je správně uvedeno v XML deklaraci. Klienti proto výstup
před zpracováním převádějí na UTF-8 (např. knihovna PHP-Pohoda-Connector).

Jmenné prostory a prefixy
-------------------------

Všechny jmenné prostory mají tvar
``http://www.stormware.cz/schema/version_2/<soubor>.xsd``. Běžně užívané
prefixy:

.. list-table::
   :header-rows: 1
   :widths: 12 28 60

   * - Prefix
     - Soubor XSD
     - Obsah
   * - ``dat``
     - data.xsd
     - obálka ``dataPack``
   * - ``rsp``
     - response.xsd
     - obálka ``responsePack``
   * - ``typ``
     - type.xsd
     - společné typy (``refType``, adresy, částky...)
   * - ``ftr``
     - filter.xsd
     - filtry pro export
   * - ``lst``
     - list.xsd
     - požadavky na výpis (``listXxxRequest``) a výpisy
   * - ``inv``
     - invoice.xsd
     - faktury
   * - ``vch``
     - voucher.xsd
     - pokladní doklady
   * - ``int``
     - intDoc.xsd
     - interní doklady
   * - ``ord``
     - order.xsd
     - objednávky
   * - ``enq`` / ``ofr``
     - enquiry.xsd / offer.xsd
     - poptávky / nabídky
   * - ``adb``
     - addressbook.xsd
     - adresář
   * - ``stk``
     - stock.xsd
     - skladové zásoby
   * - ``vyd`` / ``pri`` / ``pre`` / ``vyr`` / ``pro``
     - vydejka / prijemka / prevodka / vyroba / prodejka
     - výdejky, příjemky, převodky, výroba, prodejky
   * - ``bnk``
     - bank.xsd
     - banka
   * - ``prn``
     - print.xsd
     - tisk
   * - ``lck``
     - lock.xsd
     - zamykání dokladů
   * - ``ipm`` / ``prm``
     - intParam.xsd / parameter.xsd
     - uživatelské parametry

Úplný seznam importovaných schémat je na začátku ``data.xsd``.
