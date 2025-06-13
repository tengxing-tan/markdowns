## Send invitation email
1. Login as Ben
2. Click "Invite"
3. Fill the details.
4. Done!

## Set permission View Invitation Client
1. Login as **Hosting**
2. **Enable Feature set**: [Master data](http://localhost/EOLDev/docs/MenuMasterData.aspx?hHeaderContainer=&Menu=&_Division_=1) > [Overview | Packages](http://localhost/EOLDev/docs/LogItems.aspx?MainSupplier=&List_TO=False&Class_04=&Class_05=&List_CM=&List_lv_ps=200&Text=deb&Selector=List%3atList&Package=&List_lv_Order=0&Class_01=&ItemStatus=&_Division_=1&List_lv_Col=dCode&RememberFilter=True&IsOnDemandItem2=&Warehouse=&Mode=2&InactiveStock=False&List_lv%24pg_LastPageNumber=1&List_lv%24pg_PageNumber=1&MaxPricePrecision=&IntuitLinkedStatus=&NewPricePrecision=&List_ST=&NoDataGraphic=&MessageID=&List_SP=&Action=0&List_SR=&Class_02=) > [Package | EOLAccountancyPlusDEB - Exact Online Accountancy Plus DEB](http://localhost/EOLDev/docs/LogItemCard.aspx?CallStackAction=0&Item=%7b1767d20d-5f4a-4ddf-9c78-ada5049ec681%7d&Mode=2&Action=0&WarningMsg=&ErrorMessage=&_Division_=1) > Maintenance | Package - Parts
3. Search username. "**EOLAccountancyPlusDEB**" in this case
4. Search & enable "**ClientInviteLog**", save it.
5. Done! You can login to super Ben to see the log.

## View Invitation Client Log
1. Login as super ben
2. Choose company: "**Practice Management Company**"
3. Go to: **Accountancy: Collaboration: invitations overview**
4. Done!

## Why DB and BC are separated

Because of the concept of the EOL architecture 
- Databases -> load balances -> Web servers -> Client Browsers 
- All these are not singular, not plural! Update all machines in couple of phases.

**What is Web server:**
- IIS (Internet Information Service by Microsoft, alternative of Apache)
- Firewall (Monitor traffic)
- This server interpret files, i.e. `aspx`(half-half), `vb`, `cs`

> Therefore, DB changes only see these files: `db.xml` & `Sources/sql/invitationClientLog_AddColumn_sysmodified.sql`

