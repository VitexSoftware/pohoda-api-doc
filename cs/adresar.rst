Adresář
=======

Schéma ``addressbook.xsd`` (prefix ``adb``), element ``adb:addressbook``.

.. code-block:: xml

   <adb:addressbook version="2.0">
     <adb:addressbookHeader>
       <adb:identity>
         <typ:address>
           <typ:company>Vitex Software</typ:company>
           <typ:name>Vítězslav Dvořák</typ:name>
           <typ:city>Praha</typ:city>
           <typ:street>Dlouhá 1</typ:street>
           <typ:zip>15800</typ:zip>
           <typ:ico>69438676</typ:ico>
           <typ:dic>CZ7808072811</typ:dic>
         </typ:address>
       </adb:identity>
       <adb:mobil>739 778 202</adb:mobil>
       <adb:web>https://www.vitexsoftware.cz</adb:web>
     </adb:addressbookHeader>
   </adb:addressbook>

Prvky ``addressbookHeader`` (výběr)
-----------------------------------

``id``, ``identity`` (adresa partnera, včetně dodacích adres), ``region``,
``phone``, ``mobil``, ``fax``, ``email``, ``web``, ``adGroup`` (skupina),
``credit`` / ``creditMax`` (kredit), ``priceIDS`` (cenová hladina),
``maturity`` / ``maturityCommitments`` (splatnost), ``paymentType``,
``agreement``, ``number`` (číslo osoby), ``function``, ``salutation``,
``dateOfBirth``, ``message``, ``note`` / ``intNote``,
``accountingIssuedInvoice`` / ``accountingReceivedInvoice`` (výchozí
předkontace), ``accountForInvoicing``, ``foreignCurrency``, ``centre``,
``activity``, ``contract``, ``parameters``, ``labels``, ``carrier``.

Další bloky: bankovní účty (``addressbookAccountType``), GDPR
(``addressbookGDPRType``).

Aktualizace a vyhledání
-----------------------

Záznam se aktualizuje přes ``adb:actionType/adb:update/ftr:filter``
(:doc:`import_dat`); doporučené je filtrovat dle ``extId`` nebo IČO.
Export: ``lst:listAddressBookRequest`` (výsledek v ``lAdb:addressbook``).
