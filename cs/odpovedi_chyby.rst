Odpovědi a chyby: responsePack
==============================

Pohoda odpoví souborem ``rsp:responsePack`` se stejným ``id`` jako vstupní
``dataPack``.

.. code-block:: xml

   <rsp:responsePack version="2.0" id="imp-1" state="ok"
       ico="12345678" note="Import faktury"
       xmlns:rsp="http://www.stormware.cz/schema/version_2/response.xsd"
       xmlns:rdc="http://www.stormware.cz/schema/version_2/documentresponse.xsd"
       xmlns:inv="http://www.stormware.cz/schema/version_2/invoice.xsd"
       xmlns:typ="http://www.stormware.cz/schema/version_2/type.xsd">
     <rsp:responsePackItem version="2.0" id="FA001" state="ok">
       <inv:invoiceResponse version="2.0" state="ok">
         <rdc:producedDetails>
           <rdc:id>1234</rdc:id>
           <rdc:number>
             <typ:numberRequested>26FV0001</typ:numberRequested>
           </rdc:number>
         </rdc:producedDetails>
       </inv:invoiceResponse>
     </rsp:responsePackItem>
   </rsp:responsePack>

Atributy ``responsePack``
-------------------------

``version``, ``id``, ``state`` – povinné; ``state`` je ``ok`` nebo ``error``
(``typ:stavType2``). Dále ``note``, ``programVersion``, ``ico`` / ``key``
(firma, která XML zpracovala) a ``dateTimeStamp``.

``responsePackItem`` má vlastní ``state`` a obsahuje právě jednu odpověď
agendy (``inv:invoiceResponse``, ``adb:addressbookResponse``,
``ord:orderResponse``...). Seznam podporovaných odpovědí viz
``docs/ResponseTypes.md`` v PHP-Pohoda-Connector.

Detaily dokladu (``documentresponse.xsd``)
------------------------------------------

``rdc:importDetails``
   seznam ``rdc:detail`` s chybami a upozorněními při načtení dokladu
   (``state``, ``errno``, ``note``, případně ``XPath`` ukazující na
   problematický element).
``rdc:producedDetails``
   informace o vytvořeném / změněném záznamu: ``id``, ``number``, ``code``,
   ``actionType``.
``rdc:printDetails``
   přílohy vytvořené tiskem (``idReport`` a Base64 ``data``) – viz
   :doc:`tisk`.

Stavy
-----

* ``ok`` – záznam zpracován.
* ``warning`` – záznam byl zpracován, ale s upozorněním (objevuje se
  v ``rdc:detail`` a klienti, např. PHP-Pohoda-Connector, jej zpracovávají).
* ``error`` – záznam nebyl uložen, vysvětlení je v ``importDetails``.

.. warning::

   ``responsePack/@state="ok"`` neznamená, že byly zpracovány všechny
   položky: chyba jednoho ``dataPackItem`` se projeví v jeho
   ``responsePackItem``. Vždy kontrolujte stav každé položky.

Pohoda zpětně opakuje ``note`` z požadavku i u úspěšné odpovědi – nejde o
chybu.

Obvyklé příčiny chyb
--------------------

* ``ico`` v ``dataPack`` neodpovídá účetní jednotce, nebo ``period``
  neodpovídá aktuálnímu období.
* Neexistující odkaz (``ids`` předkontace, měny, střediska, skladu).
* Duplicitní ``id`` při zapnuté kontrole duplicit.
* Chybné kódování nebo XML neodpovídající XSD (validujte před odesláním).
* Uživatel nemá oprávnění k agendě (:doc:`mserver`).
