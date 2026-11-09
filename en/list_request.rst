Exporting (listing) data
========================

An export is a ``dataPack`` containing a ``lst:list<Agenda>Request``. The
answer is a ``responsePack`` with the list (``lst:list<Agenda>``).

Example: list of issued invoices
--------------------------------

.. code-block:: xml

   <dat:dataPack
       xmlns:dat="http://www.stormware.cz/schema/version_2/data.xsd"
       xmlns:lst="http://www.stormware.cz/schema/version_2/list.xsd"
       xmlns:ftr="http://www.stormware.cz/schema/version_2/filter.xsd"
       version="2.0" id="exp-1" ico="12345678"
       application="MyApp" note="Invoice export">
     <dat:dataPackItem version="2.0" id="L1">
       <lst:listInvoiceRequest version="2.0"
           invoiceVersion="2.0" invoiceType="issuedInvoice">
         <lst:limit>
           <ftr:count>100</ftr:count>
         </lst:limit>
         <lst:requestInvoice>
           <ftr:filter>
             <ftr:dateFrom>2026-11-01</ftr:dateFrom>
             <ftr:dateTill>2026-11-30</ftr:dateTill>
           </ftr:filter>
         </lst:requestInvoice>
       </lst:listInvoiceRequest>
     </dat:dataPackItem>
   </dat:dataPack>

Request attributes
------------------

.. list-table::
   :header-rows: 1
   :widths: 25 12 63

   * - Attribute
     - Required
     - Meaning
   * - ``version``
     - yes
     - Request version (``listInvoiceRequestVerType``).
   * - ``invoiceType``
     - yes
     - Invoice type: ``issuedInvoice``, ``issuedCreditNotice``,
       ``issuedDebitNote``, ``issuedAdvanceInvoice``, ``receivable``,
       ``issuedProformaInvoice``, ``penalty``, ``issuedCorrectiveTax``,
       ``receivedInvoice``, ``receivedCreditNotice``, ``receivedDebitNote``,
       ``receivedAdvanceInvoice``, ``commitment``,
       ``receivedProformaInvoice``, ``receivedCorrectiveTax``.
   * - ``invoiceVersion``
     - yes
     - Document version in the response.
   * - ``extSystem``
     - no
     - External system name; its ``extId`` is returned in the response.

Other agendas have analogous requests (``listCashRegisterRequest``,
``listBankAccountRequest``, ``listIntDocRequest``, ``listAddressBookRequest``,
``listStockRequest``...) – the full list is in ``list.xsd``.

Request content
---------------

``lst:limit``
   limits the record count (``ftr:count``, ``ftr:idFrom`` – export from the
   given ID, useful for paging).
``lst:request<Agenda>``
   the filter – one of:

   * ``ftr:filter`` – fields to filter on (e.g. ``id``, ``extId``,
     ``dateFrom``, ``dateTill``, ``selectedNumbers``; the set depends on the
     agenda, see ``filter.xsd``),
   * ``ftr:queryFilter`` – SQL-like condition over agenda fields,
   * ``ftr:userFilterName`` – name of a user filter stored in Pohoda.
``lst:restrictionData``
   restricts the exported document data (``restrictionDocParamType``).

Paging
------

Pohoda has no offset; page by combining ``ftr:idFrom`` (last known ``id`` + 1)
with ``ftr:count``. Documents are returned in ascending ``id`` order.
*(Unverified against a production installation – check on your version.)*
