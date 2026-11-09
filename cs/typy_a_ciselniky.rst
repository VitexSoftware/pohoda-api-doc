Společné typy a číselníky
=========================

Společné typy jsou definovány v ``type.xsd`` (prefix ``typ``).

Odkaz na záznam: ``typ:refType``
--------------------------------

.. code-block:: xml

   <inv:paymentType>
     <typ:ids>Příkazem</typ:ids>
   </inv:paymentType>

   <typ:country><typ:ids>CZ</typ:ids></typ:country>

``id``
   číselné ID Pohody (``typ:idType``, celé číslo ≥ 1, generuje Pohoda).
   Má vyšší prioritu než ostatní prvky.
``ids``
   textový identifikátor (``typ:idsType``), např. kód měny ``CZK``,
   zkratka předkontace, kód střediska.
``extId``
   identifikátor externího systému (``typ:extIdType``): ``ids`` +
   ``exSystemName``.

Adresa: ``typ:address`` / ``typ:myAddress``
-------------------------------------------

Prvky: ``company``, ``division``, ``name``, ``city``, ``street``, ``zip``,
``ico``, ``dic``, ``VATPayerType``, ``icDph`` (SK), ``country``, ``phone``,
``mobilPhone``, ``fax``, ``email``... ``partnerIdentity`` v dokladu může
obsahovat odkaz na adresář (``typ:id`` / ``typ:extId``) i přímo vloženou
adresu; ``myIdentity`` je identita vlastní firmy.

Částky a sazby DPH
------------------

* Částky v položce (``typ:typeCurrencyHomeItem``): ``unitPrice``, ``price``,
  ``priceVAT``; v domácí měně (``homeCurrency``), v cizí měně
  (``foreignCurrency``).
* Součty (``typ:typeCurrencyHome``): ``priceNone``, ``priceLow``,
  ``priceLowVAT``, ``priceHigh``, ``priceHighVAT`` ...
* ``rateVAT`` (``typ:vatRateType``): ``none``, ``high``, ``low`` (další
  hodnoty, např. pro třetí sníženou sazbu, viz ``type.xsd`` vaší verze).
* ``payVAT`` – cena v položce je s DPH (``true``) nebo bez DPH.
* ``calculateVAT`` – způsob výpočtu DPH shora / zdola.

Platba
------

``paymentType`` (``typ:paymentType``) je ``refType`` na způsob platby,
nebo výčet hodnot ``draft`` (příkazem), ``cash`` (hotově), ``postal``
(složenkou), ``delivery`` (dobírkou) – doplňte podle
``type.xsd`` / nastavení Pohody. ``account`` je bankovní účet,
``symVar`` / ``symConst`` / ``symSpec`` jsou variabilní, konstantní a
specifický symbol.

Délky řetězců
-------------

``typ:string32``, ``string64``, ``string90``, ``string240``... – maximální
délky polí. Přetečení způsobí chybu ve validaci.

Čísla dokladů
-------------

Číslo je přidělováno z číselné řady agendy; požadované číslo se v importu
zadává ``typ:numberRequested`` (viz ``numberType``), skutečně přidělené
číslo je v ``rdc:producedDetails``. Číselné řady lze spravovat vlastní
agendou ``nms:numericalSeries``.

Uživatelské parametry a štítky
------------------------------

Dokladům lze přiřadit ``labels`` (štítky) a ``parameters`` (uživatelské
parametry; definice parametrů v agendě ``intParam`` / ``parameter``).
