mServer: HTTP rozhraní
======================

**POHODA mServer** je HTTP server vestavěný do Pohody. Přijímá ``dataPack``
v těle HTTP POST a vrací ``responsePack`` – tedy totéž XML jako při souborovém
importu/exportu (:doc:`xml_format`).

Provoz
------

* Pohoda musí běžet; **jedna konfigurace mServeru obsazuje jednu instanci
  programu**, kterou nelze zároveň používat k ruční práci. Pro ruční práci
  spusťte Pohodu podruhé.
* Typické použití: mKasa, aplikace třetích stran, internetové obchody.
* Stormware doporučuje provoz na serverovém OS **ve vnitřní síti**; mServer
  nepoužívejte na stroji s veřejnou IP adresou. Komunikace je v základu
  nešifrovaná HTTP (starší dokumentace) – případné TLS řešte reverzní
  proxy.

Zdroj: `stormware.cz/pohoda/xml/mserver
<https://www.stormware.cz/pohoda/xml/mserver/>`_ (přehled); detaily níže
vycházejí z implementace klienta PHP-Pohoda-Connector.

Koncové body
------------

.. list-table::
   :header-rows: 1
   :widths: 22 78

   * - Cesta
     - Použití
   * - ``/xml``
     - POST s ``dataPack`` (import i export). Cesta se zadává **bez**
       rozlišení velikosti písmen, ale musí být uvedena; bez ní vrací
       server ``404``. Příklad: ``http://192.168.0.1:444/xml``.
   * - ``/status``
     - Kontrola dostupnosti (POST s autentizací). Odpověď obsahuje text
       ``Response from POHODA mServer`` (používá ``isOnline()``
       v PHP-Pohoda-Connector). Oficiální dokumentací *neověřeno*.

HTTP hlavičky
-------------

.. list-table::
   :header-rows: 1
   :widths: 28 72

   * - Hlavička
     - Význam
   * - ``STW-Authorization``
     - ``Basic <base64(uživatel:heslo)>`` – uživatel Pohody. Povinná.
   * - ``STW-Application``
     - Název aplikace (zobrazí se v agendě XML Import).
   * - ``STW-Instance``
     - Výběr konkrétní instance / konfigurace mServeru.
   * - ``STW-Check-Duplicity``
     - ``true`` – zapne kontrolu duplicit dle ``id`` balíku.
   * - ``Content-Type`` / ``Accept``
     - ``application/xml``

Ukázka s curl:

.. code-block:: bash

   curl -sS -X POST http://192.168.0.1:444/xml \
     -H "STW-Authorization: Basic $(printf 'user:pass' | base64)" \
     -H "STW-Application: MojeAplikace" \
     -H "Content-Type: application/xml" \
     --data-binary @datapack.xml

.. note::

   ASP/HTTP konektor pro mServer (oficiální návod Stormware) používá
   hlavičku ``Stw-Server-Name`` pro výběr serveru; v přímém volání ji
   nepoužívejte.

Kódy odpovědí
-------------

.. list-table::
   :header-rows: 1
   :widths: 12 88

   * - Kód
     - Obvyklá příčina u mServeru
   * - ``200``
     - Požadavek zpracován; stav jednotlivých záznamů je v XML odpovědi.
   * - ``400``
     - Syntakticky nesprávný požadavek (špatné XML).
   * - ``401``
     - Chybí autentizace, nebo uživatel v Pohodě neexistuje.
   * - ``403``
     - Uživatel nemá právo otevřít účetní jednotku.
   * - ``404``
     - Špatná URL – chybí cesta ``/xml``.
   * - ``405``
     - Použita jiná metoda než POST.
   * - ``408``
     - Vypršel čas zpracování.
   * - ``500``
     - Nespecifikovaná chyba při zpracování.
   * - ``502`` / ``503`` / ``504``
     - Proxy / služba nedostupná / timeout brány.

Poznámky ke klientům
--------------------

* Odpověď je ve Windows-1250 – převeďte na UTF-8.
* Nastavte rozumný timeout (výchozí v PHP-Pohoda-Connector je 30 s);
  velké exporty trvají déle.
* Komprese je volitelná (``POHODA_COMPRESS``).
