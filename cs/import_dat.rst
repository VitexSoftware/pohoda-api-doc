Import (zápis) dat
==================

Import je ``dataPack`` obsahující jeden nebo více ``dataPackItem``. Každý
``dataPackItem`` nese jeden záznam agendy (fakturu, objednávku, adresu...).

Příklad: vydaná faktura
-----------------------

.. code-block:: xml

   <?xml version="1.0" encoding="Windows-1250"?>
   <dat:dataPack
       xmlns:dat="http://www.stormware.cz/schema/version_2/data.xsd"
       xmlns:inv="http://www.stormware.cz/schema/version_2/invoice.xsd"
       xmlns:typ="http://www.stormware.cz/schema/version_2/type.xsd"
       version="2.0" id="imp-1" ico="12345678"
       application="MojeAplikace" note="Import faktury">
     <dat:dataPackItem version="2.0" id="FA001">
       <inv:invoice version="2.0">
         <inv:invoiceHeader>
           <inv:invoiceType>issuedInvoice</inv:invoiceType>
           <inv:date>2026-11-09</inv:date>
           <inv:dateTax>2026-11-09</inv:dateTax>
           <inv:dateDue>2026-11-23</inv:dateDue>
           <inv:text>Služby za listopad</inv:text>
           <inv:partnerIdentity>
             <typ:address>
               <typ:company>Vitex Software</typ:company>
               <typ:city>Praha</typ:city>
               <typ:street>Dlouhá 1</typ:street>
               <typ:zip>15800</typ:zip>
               <typ:ico>69438676</typ:ico>
             </typ:address>
           </inv:partnerIdentity>
         </inv:invoiceHeader>
         <inv:invoiceDetail>
           <inv:invoiceItem>
             <inv:text>Hodinová sazba</inv:text>
             <inv:quantity>10</inv:quantity>
             <inv:unit>h</inv:unit>
             <inv:payVAT>false</inv:payVAT>
             <inv:rateVAT>high</inv:rateVAT>
             <inv:homeCurrency>
               <typ:unitPrice>1000</typ:unitPrice>
             </inv:homeCurrency>
           </inv:invoiceItem>
         </inv:invoiceDetail>
       </inv:invoice>
     </dat:dataPackItem>
   </dat:dataPack>

Struktura záznamu agendy
------------------------

Většina agend (faktury, objednávky, interní doklady, nabídky...) má stejnou
třístupňovou kostru:

``<agenda>Header``
   hlavička dokladu (typ, data, partner, platba, středisko, poznámky...).
``<agenda>Detail``
   položky dokladu (``invoiceItem`` apod.; text, množství, jednotka, DPH,
   cena, odkaz na skladovou zásobu ``stockItem``).
``<agenda>Summary``
   součty (zaokrouhlení, měnové součty ``homeCurrency`` / ``foreignCurrency``).
   Pohoda součty vypočte sama, v importu je zpravidla není třeba posílat.

Elementy ``invoiceHeader`` jsou nepovinné (``minOccurs=0``) kromě
``invoiceType``; chybějící hodnoty Pohoda doplní z nastavení agendy
(předkontace, číselná řada, způsob úhrady...).

Typ operace (``actionType``)
----------------------------

Podle ``typ:actionTypeItem`` je ``actionType`` volba **add** (výchozí),
**update**, **delete**. U ``update`` a ``delete`` se záznam najde filtrem:

.. code-block:: xml

   <adb:addressbook version="2.0">
     <adb:actionType>
       <adb:update>
         <ftr:filter>
           <ftr:extId>
             <typ:ids>CRM-4711</typ:ids>
             <typ:exSystemName>MojeCRM</typ:exSystemName>
           </ftr:extId>
         </ftr:filter>
       </adb:update>
     </adb:actionType>
     <adb:addressbookHeader>
       <adb:phone>+420 777 000 000</adb:phone>
     </adb:addressbookHeader>
   </adb:addressbook>

Filtr ``ftr:filter`` (typ ``filterExtIdType``) umožňuje hledat podle ``id``
Pohody nebo podle ``extId`` – dvojice ``ids`` (identifikátor záznamu ve vašem
systému) a ``exSystemName`` (název externího systému; obě max. 64 znaků).
Doporučuje se při vkládání ukládat ``extId`` a dále ho používat pro
aktualizace.

U položek dokladu má ``actionType`` (``typ:actionTypeStockItem`` apod.)
vlastní význam – přidání, změna nebo smazání jedné položky při úpravě
existujícího dokladu.

Odkazy na jiné záznamy (``refType``)
-------------------------------------

Číselníky a související záznamy se uvádějí typem ``typ:refType``; jeho
elementy jsou ``id`` (číselné ID Pohody, vyšší priorita), ``ids``
(textový kód, např. zkratka předkontace, měny, střediska) a ``extId``
(identifikátor externího systému). Více v :doc:`typy_a_ciselniky`.

Kontrola duplicit
-----------------

``id`` v ``dataPack`` a ``dataPackItem`` slouží ke kontrole duplicit. Přes
mServer lze kontrolu zapnout hlavičkou ``STW-Check-Duplicity: true``
(:doc:`mserver`) – opakované odeslání téhož balíku pak Pohoda odmítne.

Další vazby a speciální operace
-------------------------------

* ``links`` – vytvoření dokladu z jiného (např. faktura z přijaté objednávky,
  faktura z výdejky).
* ``cancelDocument`` – storno dokladu.
* ``correctiveDocument`` – opravný daňový doklad (CZ) / dobropis (SK).
* ``liquidation`` – párování úhrad.
