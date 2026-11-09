Invoices
========

Schema ``invoice.xsd`` (prefix ``inv``), element ``inv:invoice``
(``version="2.0"``).

Invoice types (``invoiceType``)
-------------------------------

.. list-table::
   :header-rows: 1
   :widths: 35 65

   * - Value
     - Meaning
   * - ``issuedInvoice``
     - issued invoice
   * - ``issuedCreditNotice``
     - issued credit note
   * - ``issuedDebitNote``
     - issued debit note
   * - ``issuedAdvanceInvoice``
     - issued advance invoice
   * - ``issuedProformaInvoice``
     - issued proforma invoice
   * - ``issuedCorrectiveTax``
     - issued corrective tax document
   * - ``receivable``
     - receivable
   * - ``penalty``
     - penalty
   * - ``receivedInvoice``
     - received invoice
   * - ``receivedCreditNotice`` / ``receivedDebitNote``
     - received credit note / debit note
   * - ``receivedAdvanceInvoice`` / ``receivedProformaInvoice``
     - received advance / proforma invoice
   * - ``receivedCorrectiveTax``
     - received corrective tax document
   * - ``commitment``
     - commitment (payable)

Structure
---------

``invoiceHeader``
   ``id``, ``extId``, ``invoiceType`` (required), ``number`` (document
   number), ``symVar``, dates ``date``, ``dateTax``, ``dateAccounting``,
   ``dateDue``, ``dateDelivery``..., ``accounting`` (pre-accounting),
   ``classificationVAT``, ``text`` (up to 240 characters),
   ``partnerIdentity``, ``myIdentity``, ``paymentType``, ``account``,
   ``symConst``, ``centre``, ``activity``, ``contract``, ``note`` /
   ``intNote``, ``liquidation`` (payment), ``labels``, ``parameters``.
``invoiceDetail``
   repeating ``invoiceItem``: ``text`` (max. 90), ``quantity``, ``unit``,
   ``coefficient``, ``payVAT``, ``rateVAT``, ``percentVAT``,
   ``discountPercentage``, ``homeCurrency`` / ``foreignCurrency``
   (``unitPrice``, ``price``, ``priceVAT``), ``code`` / ``stockItem``
   (stock link), ``accounting``, ``classificationVAT``.
``invoiceSummary``
   ``roundingDocument``, ``roundingVAT``, ``calculateVAT``,
   ``typeCalculateVATInclusivePrice``, ``homeCurrency`` (totals per rate),
   ``foreignCurrency``.

Payment and links
-----------------

* Creating an invoice from another document: the ``links`` block (received
  orders, issue slips, receipts).
* Cancellation: ``cancelDocument``; corrective tax document:
  ``correctiveDocument``.
* Paying an invoice: the ``liquidation`` element in the header, or a document
  in the bank / cash agenda (:doc:`agendas`).

For an example of a received invoice with an advance and a stock item see the
`spec <https://github.com/riesenia/pohoda/tree/master/spec>`_ folder of the
riesenia/pohoda project.
