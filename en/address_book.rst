Address book
============

Schema ``addressbook.xsd`` (prefix ``adb``), element ``adb:addressbook``.

.. code-block:: xml

   <adb:addressbook version="2.0">
     <adb:addressbookHeader>
       <adb:identity>
         <typ:address>
           <typ:company>Vitex Software</typ:company>
           <typ:name>Vitezslav Dvorak</typ:name>
           <typ:city>Praha</typ:city>
           <typ:street>Dlouha 1</typ:street>
           <typ:zip>15800</typ:zip>
           <typ:ico>69438676</typ:ico>
           <typ:dic>CZ7808072811</typ:dic>
         </typ:address>
       </adb:identity>
       <adb:mobil>739 778 202</adb:mobil>
       <adb:web>https://www.vitexsoftware.cz</adb:web>
     </adb:addressbookHeader>
   </adb:addressbook>

``addressbookHeader`` elements (selection)
------------------------------------------

``id``, ``identity`` (partner address, including delivery addresses),
``region``, ``phone``, ``mobil``, ``fax``, ``email``, ``web``, ``adGroup``
(group), ``credit`` / ``creditMax``, ``priceIDS`` (price level),
``maturity`` / ``maturityCommitments`` (due periods), ``paymentType``,
``agreement``, ``number`` (person number), ``function``, ``salutation``,
``dateOfBirth``, ``message``, ``note`` / ``intNote``,
``accountingIssuedInvoice`` / ``accountingReceivedInvoice`` (default
pre-accounting), ``accountForInvoicing``, ``foreignCurrency``, ``centre``,
``activity``, ``contract``, ``parameters``, ``labels``, ``carrier``.

Further blocks: bank accounts (``addressbookAccountType``), GDPR
(``addressbookGDPRType``).

Updating and lookup
-------------------

A record is updated via ``adb:actionType/adb:update/ftr:filter``
(:doc:`import_data`); filtering by ``extId`` or company ID is recommended.
Export: ``lst:listAddressBookRequest`` (result in ``lAdb:addressbook``).
