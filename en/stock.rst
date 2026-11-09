Stock and warehouses
====================

Schema ``stock.xsd`` (prefix ``stk``), element ``stk:stock``; the answer is
``stk:stockItemResponse``. Stock documents have their own agendas: issue
slips (``vyd``), receipts (``pri``), transfers (``pre``), production
(``vyr``), sales slips (``pro``).

Stock header (``stockHeader``, selection)
-----------------------------------------

``id``, ``extId``, ``stockType`` (card, service, set, ...), ``code`` (stock
code), ``EAN``, ``PLU``, ``isSales``, ``isSerialNumber``, ``isInternet``,
``isBatch``, ``purchasingRateVAT``, ``sellingRateVAT``, ``name``,
``nameComplement``, ``unit``, ``storage`` (store breakdown), ``typePrice``,
``weightedPurchasePrice``, ``purchasingPrice``, ``sellingPrice`` and many
more (see ``stock.xsd``).

Other blocks: ``stockPriceItem`` (price levels), ``stockSerialNumber``
(serial numbers), ``stockAttach`` (attachments), ``stockInfo``.

Referencing stock in a document
-------------------------------

A document item refers to stock like this:

.. code-block:: xml

   <inv:invoiceItem>
     <inv:text>Cable</inv:text>
     <inv:quantity>2</inv:quantity>
     <inv:stockItem>
       <typ:stockItem>
         <typ:ids>KAB001</typ:ids>
       </typ:stockItem>
     </inv:stockItem>
   </inv:invoiceItem>

``typ:stockItemType`` optionally contains ``store``, a required
``stockItem`` (``typ:stockRefType``) and ``serialNumber``.

Exporting stock
---------------

``lst:listStockRequest`` → ``lStk:stock``; stock levels are returned by
``lst:listStockRequest`` / ``lst:listStoresRequest`` (see ``list.xsd``,
``list_stock.xsd``).
