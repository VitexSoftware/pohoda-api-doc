Export (výpis) dat
==================

Export je ``dataPack`` obsahující požadavek ``lst:list<Agenda>Request``.
Odpověď je ``responsePack`` s výpisem (``lst:list<Agenda>``).

Příklad: seznam vydaných faktur
-------------------------------

.. code-block:: xml

   <dat:dataPack
       xmlns:dat="http://www.stormware.cz/schema/version_2/data.xsd"
       xmlns:lst="http://www.stormware.cz/schema/version_2/list.xsd"
       xmlns:ftr="http://www.stormware.cz/schema/version_2/filter.xsd"
       version="2.0" id="exp-1" ico="12345678"
       application="MojeAplikace" note="Export faktur">
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

Atributy požadavku
------------------

.. list-table::
   :header-rows: 1
   :widths: 25 12 63

   * - Atribut
     - Povinný
     - Význam
   * - ``version``
     - ano
     - Verze požadavku (``listInvoiceRequestVerType``).
   * - ``invoiceType``
     - ano
     - Typ faktury: ``issuedInvoice``, ``issuedCreditNotice``,
       ``issuedDebitNote``, ``issuedAdvanceInvoice``, ``receivable``,
       ``issuedProformaInvoice``, ``penalty``, ``issuedCorrectiveTax``,
       ``receivedInvoice``, ``receivedCreditNotice``, ``receivedDebitNote``,
       ``receivedAdvanceInvoice``, ``commitment``,
       ``receivedProformaInvoice``, ``receivedCorrectiveTax``.
   * - ``invoiceVersion``
     - ano
     - Verze dokladu v odpovědi.
   * - ``extSystem``
     - ne
     - Označení externího systému; v odpovědi se vrátí jeho ``extId``.

Další agendy mají obdobné požadavky (``listCashRegisterRequest``,
``listBankAccountRequest``, ``listIntDocRequest``, ``listAddressBookRequest``,
``listStockRequest``...) – kompletní seznam je v ``list.xsd``.

Obsah požadavku
---------------

``lst:limit``
   omezení počtu záznamů (``ftr:count``, ``ftr:idFrom`` – export od zadaného
   ID, vhodné pro stránkování).
``lst:request<Agenda>``
   filtr – jedna z možností:

   * ``ftr:filter`` – pole k filtrování (např. ``id``, ``extId``,
     ``dateFrom``, ``dateTill``, ``selectedNumbers``; sada polí závisí
     na agendě, viz ``filter.xsd``),
   * ``ftr:queryFilter`` – SQL-like podmínka nad poli agendy,
   * ``ftr:userFilterName`` – název uživatelského filtru uloženého v Pohodě.
``lst:restrictionData``
   omezení množiny exportovaných dat dokladů (``restrictionDocParamType``).

Stránkování
-----------

Pohoda nemá offset; stránkuje se kombinací ``ftr:idFrom`` (poslední známé
``id`` + 1) a ``ftr:count``. Doklady jsou vraceny podle rostoucího ``id``.
*(Neověřeno proti produkční instalaci – ověřte na své verzi.)*
