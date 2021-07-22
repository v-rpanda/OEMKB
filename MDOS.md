**Title: 5-54564576\_\[EXTERNAL\] Bangho \| Office H&B 2019 Bidding
Process (Ocasa) CRM:58756**

**Description**: Customer is reporting us that they are having some
issues to activate Office Home & Business 2019

 According to SDOC Cloud report,

All PKIDs are ACTIVATION ENABLED status

All Service IDs are ASSIGNED status.

 Is it correct that Service IDs keep as ASSIGNED status?

**Solution:** 1) Conveyed to partner that key status of Window PKID will
not change after getting bundled with service keys. It will remain same
as the previous state it was.

2)The Bound state of the Window PKID will change from 'Not Bound' to
'Bound'.

3)After getting bundled with Window PKIDs, the key state of Service Id
will change to Product Bound.

4)Still partner was having assigned status.

5)Checked and validated that these PBRs mentioned are submitted outside
MDOS, as I don't see the MSReportuniqueIds are present in MDOS.

6)Prepared script to update service keys to product Bound and window
keys IS Bound =1.

Before updating the status in MDOS must check below point.

-   Check the windows and service key status is product bound or not in
    DOC. If yes, then take approval from Sinead or Katie to update the
    status in MDOS.

**Database Operations:**

Script to update service keys:

select \* from productkey(nolock) where MSFTProductKeyId in ('\...List
of keys\....')

Begin Tran

\--update \[ProductKey\] set KeyStateID=18 , IsBound=1 where
MSFTProductKeyId In ('\...list of keys')

\--Update Kh set kh.KeyStateID=18 from keyhistory kh inner join
productkey pk

on pk.LastKeyHistoryId = kh.KeyHistoryId

where pk.MSFTProductKeyId In ('\...\...List of keys\...')

\--Rollback tran

\--Commit tran

Script to update window key isbound=1:

Select \* from ProductKey(nolock) where MSFTProductKeyId in ('\...list
of keys\...')

Begin Tran

\--update \[ProductKey\] set IsBound= 1  where MSFTProductKeyId In
(\'\...list of keys\...')

\--Rollback tran

\--Commit tran

**CRM Reference numbers:** CRM00450308, CRM006139000
