Agendy Pohody
=============

XML rozhraní pokrývá většinu agend Pohody. Každá agenda má vlastní XSD a
jmenný prostor (:doc:`xml_format`). Tabulka níže ukazuje, kde hledat
nejčastější z nich.

Agendy dostupné přes XML
------------------------

.. list-table::
   :header-rows: 1
   :widths: 30 12 30 28

   * - Agenda
     - Prefix
     - Element záznamu / odpovědi
     - XSD
   * - Faktury (vydané, přijaté, zálohové, ...)
     - ``inv``
     - ``inv:invoice`` / ``inv:invoiceResponse``
     - invoice.xsd
   * - Pokladní doklady
     - ``vch``
     - ``vch:voucher``
     - voucher.xsd
   * - Interní doklady
     - ``int``
     - ``int:intDoc``
     - intDoc.xsd
   * - Objednávky přijaté / vydané
     - ``ord``
     - ``ord:order``
     - order.xsd
   * - Nabídky, poptávky
     - ``ofr``, ``enq``
     - ``ofr:offer``, ``enq:enquiry``
     - offer.xsd, enquiry.xsd
   * - Adresář
     - ``adb``
     - ``adb:addressbook``
     - addressbook.xsd
   * - Skladové zásoby
     - ``stk``
     - ``stk:stock``
     - stock.xsd
   * - Výdejky, příjemky, převodky, výroba, prodejky
     - ``vyd``, ``pri``, ``pre``, ``vyr``, ``pro``
     - ``vyd:vydejka`` ...
     - vydejka.xsd ...
   * - Banka
     - ``bnk``
     - ``bnk:bank``
     - bank.xsd
   * - Smlouvy
     - ``con``
     - ``con:contract``
     - contract.xsd
   * - Kategorie, sklady, skupiny zásob
     - ``ctg``, ``str``, ``grs``
     - ``ctg:category`` ...
     - category.xsd, storage.xsd, groupStocks.xsd
   * - Číselné řady
     - ``nms``
     - ``nms:numericalSeries``
     - numericalSeries.xsd
   * - Uživatelské parametry
     - ``ipm``, ``prm``
     - ``ipm:intParam``
     - intParam.xsd, parameter.xsd
   * - Tisk, zámky
     - ``prn``, ``lck``
     - ``prn:print``, ``lck:lock``
     - print.xsd, lock.xsd

Úplný soubor schémat (73 XSD) obsahuje také mzdové a personální agendy
(``absence``, ``wageElements``), EET / mKasa, GDPR, spotřební vazby
(``recyclingContrib``, ``GPSR``) a další; viz ``data.xsd``.

Seznam všech agend (číslo ``idAgend`` v SQL)
--------------------------------------------

Číslo agendy se používá v SQL databázi (např. v tabulkách příloh a historie)
– viz :doc:`sql_databaze`. Seznam vychází z projektu
php-spojenet-pohoda-sql (``idAgend.md``).

.. list-table::
   :header-rows: 1
   :widths: 8 46 46

   * - ID
     - Agenda
     - English name
   * - 1
     - Peněžní deník
     - Cash Journal
   * - 2
     - Vydané faktury
     - Issued invoices
   * - 3
     - Přijaté faktury
     - Received invoices
   * - 4
     - Drobný majetek
     - Minor assets
   * - 5
     - Dlouhodobý majetek
     - Fixed assets
   * - 6
     - Příjemky
     - Receipts
   * - 7
     - Výdejky
     - Disbursements
   * - 8
     - Převod
     - Transfer
   * - 9
     - Výroba
     - Production
   * - 10
     - Prodejna
     - Shop
   * - 11
     - Přijaté objednávky
     - Orders received
   * - 12
     - Vydané objednávky
     - Orders issued
   * - 13
     - Adresář
     - Address book
   * - 14
     - Příkazy k úhradě
     - Payment orders
   * - 15
     - Deník jízd
     - Trip log
   * - 16
     - Evidence vozidel
     - Vehicle registration
   * - 17
     - Mzdy
     - Wages
   * - 18
     - Ostatní pohledávky
     - Other receivables
   * - 19
     - Ostatní závazky
     - Other commitments
   * - 20
     - Zásoby
     - Stocks
   * - 21
     - Skladové soupravy
     - Stock kits
   * - 22
     - Cenové skupiny
     - Price groups
   * - 24
     - Přístupová práva
     - Access rights
   * - 25
     - Personalistika
     - HR
   * - 27
     - Pokladna
     - Cash register
   * - 28
     - Banka
     - Banka
   * - 29
     - Interní doklady
     - Internal documents
   * - 30
     - Likvidace
     - Disposal
   * - 31
     - Účetní deník
     - Financial Diary
   * - 32
     - Účtová osnova
     - Chart of accounts
   * - 33
     - Předkontace
     - Advance payment
   * - 34
     - Kódy bank
     - Bank codes
   * - 35
     - Číselné řady
     - Number series
   * - 36
     - Konstantní symboly
     - Constant symbols
   * - 37
     - Činnosti
     - Activities
   * - 38
     - Střediska
     - Centers
   * - 39
     - Zakázky
     - Orders
   * - 40
     - Členění DPH
     - VAT breakdown
   * - 41
     - Bankovní účty
     - Bank accounts
   * - 42
     - Uživatelské nastavení
     - User settings
   * - 43
     - Vydané zálohové faktury
     - Advance invoices issued
   * - 44
     - Přijaté zálohové faktury
     - Advance invoices received
   * - 45
     - Účetní jednotky
     - Accounting units
   * - 46
     - Obce a PSČ
     - Municipality and zip code
   * - 47
     - Globální nastavení
     - Global settings
   * - 48
     - Země
     - Earth
   * - 49
     - Skupiny
     - Groups
   * - 50
     - Klíče
     - Keys
   * - 51
     - Závazky
     - Liabilities
   * - 52
     - Prodejní ceny
     - Sale prices
   * - 53
     - Výdej
     - Delivery
   * - 54
     - Příjem
     - Income
   * - 55
     - Pohyby
     - Moves
   * - 56
     - Zdravotní pojišťovny
     - Health insurance
   * - 57
     - Sklady
     - Warehouses
   * - 58
     - Členění skladů
     - Division of warehouses
   * - 59
     - Předkontace
     - Advance payment
   * - 60
     - Umístění majetku
     - Property location
   * - 61
     - Odpisové plány
     - Depreciation plans
   * - 62
     - Položky
     - Items
   * - 63
     - Počáteční stavy účtů
     - Initial account balances
   * - 64
     - Výchozí stavy účtů
     - Default Account Statuses
   * - 65
     - Seznam řidičů
     - List of drivers
   * - 69
     - Počáteční stavy salda
     - Initial balances
   * - 71
     - Homebanking
     - Home banking
   * - 72
     - Cizí měny
     - Foreign currencies
   * - 75
     - Kursový lístek
     - Course ticket
   * - 76
     - Přiznání DPH
     - VAT return
   * - 77
     - Hotovostní pokladny
     - Cash registers
   * - 78
     - Analýza
     - Analysis
   * - 79
     - Leasingový majetek
     - Leased property
   * - 80
     - Hardware
     - Hardware
   * - 81
     - Saldo
     - Balance
   * - 82
     - Loňský stav výsledkových účtů
     - Last year's state of profit and loss accounts
   * - 83
     - Měrné jednotky
     - Units of measure
   * - 84
     - Penzijní fondy
     - Pension funds
   * - 85
     - Legislativa
     - Legislation
   * - 86
     - Internetové obchody
     - Online stores
   * - 88
     - Výrobní čísla
     - Production numbers
   * - 89
     - Životní pojišťovny
     - Life insurance companies
   * - 90
     - Kasy
     - Cash registers
   * - 91
     - Inventura
     - Stock-taking
   * - 92
     - Nabídky
     - Offers
   * - 93
     - Události
     - Events
   * - 94
     - Pobočky
     - Branches
   * - 96
     - Nepeněžní deník
     - Non-monetary diary
   * - 97
     - Poptávky
     - Requests
   * - 98
     - Výkazy minulého roku
     - Last year's statements
