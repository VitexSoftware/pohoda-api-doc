Responses and errors: responsePack
==================================

Pohoda answers with an ``rsp:responsePack`` file carrying the same ``id`` as
the incoming ``dataPack``.

.. code-block:: xml

   <rsp:responsePack version="2.0" id="imp-1" state="ok"
       ico="12345678" note="Invoice import"
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

``responsePack`` attributes
---------------------------

``version``, ``id``, ``state`` are required; ``state`` is ``ok`` or ``error``
(``typ:stavType2``). Also ``note``, ``programVersion``, ``ico`` / ``key``
(the company that processed the XML) and ``dateTimeStamp``.

``responsePackItem`` has its own ``state`` and contains exactly one agenda
response (``inv:invoiceResponse``, ``adb:addressbookResponse``,
``ord:orderResponse``...). The supported responses are listed in
``docs/ResponseTypes.md`` of PHP-Pohoda-Connector.

Document details (``documentresponse.xsd``)
-------------------------------------------

``rdc:importDetails``
   a list of ``rdc:detail`` with errors and warnings raised while loading
   the document (``state``, ``errno``, ``note``, possibly an ``XPath``
   pointing to the offending element).
``rdc:producedDetails``
   information on the created / changed record: ``id``, ``number``,
   ``code``, ``actionType``.
``rdc:printDetails``
   attachments produced by printing (``idReport`` and Base64 ``data``) –
   see :doc:`print`.

States
------

* ``ok`` – record processed.
* ``warning`` – processed with a warning (appears in ``rdc:detail``; clients
  such as PHP-Pohoda-Connector handle it).
* ``error`` – record not saved; the reason is in ``importDetails``.

.. warning::

   ``responsePack/@state="ok"`` does not mean all items succeeded: an error in
   one ``dataPackItem`` shows in its ``responsePackItem``. Always check the
   state of every item.

Pohoda echoes the request ``note`` back even in a successful response – this
is not an error.

Common causes of errors
-----------------------

* ``ico`` in ``dataPack`` does not match the accounting unit, or ``period``
  differs from the current period.
* Non-existent reference (``ids`` of a pre-accounting, currency, centre,
  store).
* Duplicate ``id`` with duplicate checking enabled.
* Wrong encoding, or XML not matching the XSD (validate before sending).
* The user lacks permission for the agenda (:doc:`mserver`).
