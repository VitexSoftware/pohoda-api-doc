Faktury
=======

Schéma ``invoice.xsd`` (prefix ``inv``), element ``inv:invoice``
(``version="2.0"``).

Typy faktur (``invoiceType``)
-----------------------------

.. list-table::
   :header-rows: 1
   :widths: 35 65

   * - Hodnota
     - Význam
   * - ``issuedInvoice``
     - vydaná faktura
   * - ``issuedCreditNotice``
     - vydaný dobropis
   * - ``issuedDebitNote``
     - vydaný vrubopis
   * - ``issuedAdvanceInvoice``
     - vydaná zálohová faktura (zálohový list)
   * - ``issuedProformaInvoice``
     - vydaná proforma faktura
   * - ``issuedCorrectiveTax``
     - vydaný opravný daňový doklad
   * - ``receivable``
     - pohledávka
   * - ``penalty``
     - penále
   * - ``receivedInvoice``
     - přijatá faktura
   * - ``receivedCreditNotice`` / ``receivedDebitNote``
     - přijatý dobropis / vrubopis
   * - ``receivedAdvanceInvoice`` / ``receivedProformaInvoice``
     - přijatá zálohová / proforma
   * - ``receivedCorrectiveTax``
     - přijatý opravný daňový doklad
   * - ``commitment``
     - závazek

Struktura
---------

``invoiceHeader``
   ``id``, ``extId``, ``invoiceType`` (povinný), ``number`` (číslo dokladu),
   ``symVar``, data ``date``, ``dateTax``, ``dateAccounting``, ``dateDue``,
   ``dateDelivery``..., ``accounting`` (předkontace), ``classificationVAT``
   (členění DPH), ``text`` (až 240 znaků), ``partnerIdentity``,
   ``myIdentity``, ``paymentType``, ``account``, ``symConst``,
   ``centre`` (středisko), ``activity`` (činnost), ``contract`` (zakázka),
   ``note`` / ``intNote``, ``liquidation`` (úhrada), ``labels``,
   ``parameters``.
``invoiceDetail``
   opakující se ``invoiceItem``: ``text`` (max. 90), ``quantity``, ``unit``,
   ``coefficient``, ``payVAT``, ``rateVAT``, ``percentVAT``,
   ``discountPercentage``, ``homeCurrency`` / ``foreignCurrency``
   (``unitPrice``, ``price``, ``priceVAT``), ``code`` / ``stockItem``
   (vazba na zásobu), ``accounting``, ``classificationVAT``.
``invoiceSummary``
   ``roundingDocument``, ``roundingVAT``, ``calculateVAT``,
   ``typeCalculateVATInclusivePrice``, ``homeCurrency`` (součty po
   sazbách), ``foreignCurrency``.

Úhrada a vazby
--------------

* Vytvoření faktury z jiného dokladu: blok ``links`` (přijaté objednávky,
  výdejky, příjemky).
* Storno: ``cancelDocument``; opravný daňový doklad: ``correctiveDocument``.
* Úhrada faktury: element ``liquidation`` v hlavičce, případně doklad
  v agendě banka / pokladna (:doc:`agendy`).

Příklad: přijatá faktura se zálohou a skladovou položkou viz
`spec <https://github.com/riesenia/pohoda/tree/master/spec>`_ projektu
riesenia/pohoda.
