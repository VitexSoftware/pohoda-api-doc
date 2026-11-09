XML format: dataPack
====================

All communication with Pohoda is an exchange of **dataPack → responsePack**
pairs.

Root element
------------

.. code-block:: xml

   <?xml version="1.0" encoding="Windows-1250"?>
   <dat:dataPack
       xmlns:dat="http://www.stormware.cz/schema/version_2/data.xsd"
       xmlns:inv="http://www.stormware.cz/schema/version_2/invoice.xsd"
       xmlns:typ="http://www.stormware.cz/schema/version_2/type.xsd"
       version="2.0" id="import-0001" ico="12345678"
       application="MyApp" note="Invoice import">
     <dat:dataPackItem version="2.0" id="FA-0001">
       <!-- exactly one agenda element -->
     </dat:dataPackItem>
   </dat:dataPack>

``dataPack`` attributes (per ``data.xsd``)
------------------------------------------

.. list-table::
   :header-rows: 1
   :widths: 20 12 68

   * - Attribute
     - Required
     - Meaning
   * - ``version``
     - yes
     - Package version. Allowed: ``1.0``, ``1.1``, ``1.2``, ``2.0``.
   * - ``id``
     - yes
     - Package identifier (max. 64 characters). Together with the item
       ``id`` it is used for duplicate import detection.
   * - ``ico``
     - no
     - Company ID the XML is meant for; must match the accounting unit's
       IČO. Takes precedence over ``key``.
   * - ``key``
     - no
     - Unique accounting key; used when ``ico`` is absent.
   * - ``period``
     - no
     - Accounting period. If omitted, the logged-in user's current period
       is used; if given and different, the communication ends with an
       error.
   * - ``application``
     - yes
     - Text shown in the *Application* field of the XML Import agenda.
   * - ``note``
     - yes
     - Note shown in the *Notes* tab of the XML Import agenda.
   * - ``programVersion``
     - no
     - Informational program version.

Each ``dataPackItem`` has required ``version`` (``1.0`` or ``2.0``) and
``id`` (max. 64 characters, unique within the package) and contains **exactly
one** agenda element (``xsd:any`` – the envelope does not validate content).

The optional ``<dat:transformation>`` element (since ``dataPack`` 1.1) sets
an XSL transformation of the input (``input``) and output (``output``).

Encoding
--------

Pohoda always produces XML in **Windows-1250**. Input may use another
encoding if declared correctly in the XML declaration. Clients therefore
convert output to UTF-8 before processing (e.g. the PHP-Pohoda-Connector).

Namespaces and prefixes
-----------------------

All namespaces take the form
``http://www.stormware.cz/schema/version_2/<file>.xsd``. Commonly used
prefixes:

.. list-table::
   :header-rows: 1
   :widths: 12 28 60

   * - Prefix
     - XSD file
     - Content
   * - ``dat``
     - data.xsd
     - ``dataPack`` envelope
   * - ``rsp``
     - response.xsd
     - ``responsePack`` envelope
   * - ``typ``
     - type.xsd
     - common types (``refType``, addresses, amounts...)
   * - ``ftr``
     - filter.xsd
     - export filters
   * - ``lst``
     - list.xsd
     - list requests (``listXxxRequest``) and lists
   * - ``inv``
     - invoice.xsd
     - invoices
   * - ``vch``
     - voucher.xsd
     - cash vouchers
   * - ``int``
     - intDoc.xsd
     - internal documents
   * - ``ord``
     - order.xsd
     - orders
   * - ``enq`` / ``ofr``
     - enquiry.xsd / offer.xsd
     - enquiries / offers
   * - ``adb``
     - addressbook.xsd
     - address book
   * - ``stk``
     - stock.xsd
     - stock items
   * - ``vyd`` / ``pri`` / ``pre`` / ``vyr`` / ``pro``
     - vydejka / prijemka / prevodka / vyroba / prodejka
     - issue slips, receipts, transfers, production, sales slips
   * - ``bnk``
     - bank.xsd
     - bank
   * - ``prn``
     - print.xsd
     - printing
   * - ``lck``
     - lock.xsd
     - document locking
   * - ``ipm`` / ``prm``
     - intParam.xsd / parameter.xsd
     - user parameters

The full list of imported schemas is at the top of ``data.xsd``.
