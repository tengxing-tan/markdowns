# Remove Obsolete Functionality
- Hide access point on UI
- 

# RRT Failing Test Investigation
- Check history, point out if the failure cause by a Pull Request.
- Run in local with same branch, same db template. 
	- if success, then request run again RRT
	- if fail, then [[#Takeout from RRT]], with two PR: master & acceptance/production.

## Takeout from RRT
```cs
// INT test
using Exact.Tests.Shared.TestCategories;
[TestMethod, Manual]
```
# Exact library
## Guard
```cs
// service
Guard.Positive(division, nameof(division));
Guard.NotEmpty(accountId, nameof(accountId));
```

## `RenderDirtyCheck`
To show a confirmation popup if there is unsaved field change. 
```vb
RenderDirtyCheck = DirtyCheck.IsDirty ' Chrome might have some issues
RenderDirtyCheck = DirtyCheck.Yes 
RenderDirtyCheck = DirtyCheck.No 
```

## `SubmitAction`
To separate client-side & server-side logic, real-time updates & no reload needed (user experience)
A button with on click event:
```aspx
<button onClick="SubmitAction(self, 'HandleClick');">Click</button>
```
- `SubmitAction (js)` - action manager
- `self` - action target
- `HandleClick (vb)` - action method

The server-side logic in ASP code behind. 
```vb
<Actino("HandleClick")>
Protected Sub HandleClick()
	' server-side logic
End Sub
```

---

# Hosting Setting
- Once your restore latest DB template, a lot of hosting setting you set before will be gone.
- Go through this checklist to make sure everything good. 

**Development/Repository is empty?** 
- [ ] Go to Hosting settings > tab "Database", 
- [ ] find "Update repository in database", check it. 
- [ ] Run DB Updater

**SSRS setup**
- [ ] Go to Hosting settings > tab "Background task", 
- [ ] find "Service URL", fill "http://localhost/ReportServer"

# Practice Management 

**Change planning start date, to generate planning start from specified date**
```sql
insert into settings(ID, Type, SettingName, ValueType, DateValue, TopicTime)
Values (NEWID(), 0, 'PMPlanningStartDate', 3, '2024-07-01 00:00:00.000', 0)
```

# Read Confluence
- [Add feature set or function point to Exact Online](https://exact-software.atlassian.net/wiki/spaces/BACTEAM/pages/1536524905/Add+featureset+or+function+point+to+Exact+Online#Create-new-feature-set-and-generate-FeatureSets.xml)
- [FSR: Final Security Review](https://exact-software.atlassian.net/wiki/spaces/PAYROLLTEAM/pages/5398986761/NFR+Tax+3PD+-+Final+security+review)


