Sklady a zásoby
===============

Schéma ``stock.xsd`` (prefix ``stk``), element ``stk:stock``; odpověď
``stk:stockItemResponse``. Skladové doklady mají vlastní agendy:
výdejky (``vyd``), příjemky (``pri``), převodky (``pre``), výroba (``vyr``),
prodejky (``pro``).

Hlavička zásoby (``stockHeader``, výběr)
----------------------------------------

``id``, ``extId``, ``stockType`` (typ zásoby: karta, služba, soubor, ...),
``code`` (skladové označení), ``EAN``, ``PLU``, ``isSales``,
``isSerialNumber``, ``isInternet``, ``isBatch``, ``purchasingRateVAT``,
``sellingRateVAT``, ``name``, ``nameComplement``, ``unit``, ``storage``
(členění skladů), ``typePrice``, ``weightedPurchasePrice``,
``purchasingPrice``, ``sellingPrice`` a další (obsáhlé, viz ``stock.xsd``).

Další bloky: ``stockPriceItem`` (cenové hladiny), ``stockSerialNumber``
(výrobní čísla), ``stockAttach`` (přílohy), ``stockInfo``.

Odkaz na zásobu v dokladu
-------------------------

V položce dokladu se zásoba označuje:

.. code-block:: xml

   <inv:invoiceItem>
     <inv:text>Kabel</inv:text>
     <inv:quantity>2</inv:quantity>
     <inv:stockItem>
       <typ:stockItem>
         <typ:ids>KAB001</typ:ids>
       </typ:stockItem>
     </inv:stockItem>
   </inv:invoiceItem>

``typ:stockItemType`` obsahuje volitelně ``store`` (sklad), povinně
``stockItem`` (``typ:stockRefType``) a ``serialNumber``.

Export zásob
------------

``lst:listStockRequest`` → ``lStk:stock``; stavy zásob vrací požadavek
na ``lst:listStockRequest`` / ``lst:listStoresRequest`` (viz ``list.xsd``,
``list_stock.xsd``).
