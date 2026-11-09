Tisk a přílohy
==============

Schéma ``print.xsd`` (prefix ``prn``), element ``prn:print``; odpověď
``prn:printResponse`` s ``rdc:printDetails``.

Pomocí tohoto požadavku lze nechat Pohodu vytisknout sestavu k záznamu na
tiskárnu, vygenerovat PDF, uložit do souboru nebo odeslat e-mailem.

Prvky (``print.xsd``, výběr)
----------------------------

``record``
   záznam, který se tiskne (agenda + ``id``).
``printerSettings``
   ``report`` (sestava, ``id``), ``printer``, ``pdf``
   (``fileName``, ``binaryData`` – vrátit data v odpovědi), ``parameters``.
``sendMail``
   e-mailové odeslání: ``to``, ``cc``, ``bcc``, ``subject``, ``body``,
   ``attachments``, ``priority``, ``returnReceipt``, ``disposNotif``.
``isdoc``
   export do formátu ISDOC (také samostatné schéma ``isdoc.xsd``).

Odpověď obsahuje ``rdc:attachment`` s ``rdc:idReport`` a Base64
``rdc:data`` (atribut ``fileName``, ``code="base64"``).

.. note::

   Přesné povinné prvky jsou proti ``print.xsd`` vaší verze. Příklad
   volání je v knihovně Riesenia Pohoda (``PrintRequest``).

Přílohy dokladů
---------------

Přílohy záznamů jsou v SQL tabulkách ``DOC`` / ``DocDirs`` a v XML se
zakládají prvky ``attachments`` v dokladech (např. ``stockAttach``).
