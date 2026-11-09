Importing (writing) data
========================

An import is a ``dataPack`` with one or more ``dataPackItem`` elements. Each
``dataPackItem`` carries one agenda record (invoice, order, address...).

Example: issued invoice
-----------------------

.. code-block:: xml

   <?xml version="1.0" encoding="Windows-1250"?>
   <dat:dataPack
       xmlns:dat="http://www.stormware.cz/schema/version_2/data.xsd"
       xmlns:inv="http://www.stormware.cz/schema/version_2/invoice.xsd"
       xmlns:typ="http://www.stormware.cz/schema/version_2/type.xsd"
       version="2.0" id="imp-1" ico="12345678"
       application="MyApp" note="Invoice import">
     <dat:dataPackItem version="2.0" id="FA001">
       <inv:invoice version="2.0">
         <inv:invoiceHeader>
           <inv:invoiceType>issuedInvoice</inv:invoiceType>
           <inv:date>2026-11-09</inv:date>
           <inv:dateTax>2026-11-09</inv:dateTax>
           <inv:dateDue>2026-11-23</inv:dateDue>
           <inv:text>Services for November</inv:text>
           <inv:partnerIdentity>
             <typ:address>
               <typ:company>Vitex Software</typ:company>
               <typ:city>Praha</typ:city>
               <typ:street>Dlouha 1</typ:street>
               <typ:zip>15800</typ:zip>
               <typ:ico>69438676</typ:ico>
             </typ:address>
           </inv:partnerIdentity>
         </inv:invoiceHeader>
         <inv:invoiceDetail>
           <inv:invoiceItem>
             <inv:text>Hourly rate</inv:text>
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

Record structure
----------------

Most agendas (invoices, orders, internal documents, offers...) share a
three-part skeleton:

``<agenda>Header``
   document header (type, dates, partner, payment, centre, notes...).
``<agenda>Detail``
   document items (``invoiceItem`` etc.; text, quantity, unit, VAT, price,
   reference to a stock item ``stockItem``).
``<agenda>Summary``
   totals (rounding, currency totals ``homeCurrency`` / ``foreignCurrency``).
   Pohoda computes totals itself, so they usually need not be sent.

``invoiceHeader`` elements are optional (``minOccurs=0``) except
``invoiceType``; missing values are filled in by Pohoda from the agenda
settings (pre-accounting, number series, payment type...).

Action type (``actionType``)
----------------------------

Per ``typ:actionTypeItem``, ``actionType`` is a choice of **add** (default),
**update**, **delete**. ``update`` and ``delete`` locate the record with a
filter:

.. code-block:: xml

   <adb:addressbook version="2.0">
     <adb:actionType>
       <adb:update>
         <ftr:filter>
           <ftr:extId>
             <typ:ids>CRM-4711</typ:ids>
             <typ:exSystemName>MyCRM</typ:exSystemName>
           </ftr:extId>
         </ftr:filter>
       </adb:update>
     </adb:actionType>
     <adb:addressbookHeader>
       <adb:phone>+420 777 000 000</adb:phone>
     </adb:addressbookHeader>
   </adb:addressbook>

The ``ftr:filter`` (type ``filterExtIdType``) finds records by Pohoda's ``id``
or by ``extId`` – the pair ``ids`` (record identifier in your system) and
``exSystemName`` (external system name; both max. 64 characters). Store an
``extId`` on insert and use it for later updates.

On document items ``actionType`` (``typ:actionTypeStockItem`` etc.) has its
own meaning – adding, changing or deleting a single item when editing an
existing document.

References to other records (``refType``)
-----------------------------------------

Code lists and related records use ``typ:refType`` with ``id`` (Pohoda
numeric ID, higher priority), ``ids`` (text code, e.g. pre-accounting
abbreviation, currency, centre) and ``extId`` (external system
identifier). See :doc:`types_and_codes`.

Duplicate detection
-------------------

The ``id`` in ``dataPack`` and ``dataPackItem`` is used for duplicate
detection. Over mServer it can be enabled with the header
``STW-Check-Duplicity: true`` (:doc:`mserver`) – Pohoda then rejects a
re-sent package.

Links and special operations
----------------------------

* ``links`` – create a document from another (e.g. invoice from a received
  order, invoice from an issue slip).
* ``cancelDocument`` – cancel a document.
* ``correctiveDocument`` – corrective tax document (CZ) / credit note (SK).
* ``liquidation`` – payment pairing.
