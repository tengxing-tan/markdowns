```
index=EOL sourcetype=EOL_Activitylog App="AccLinkAccountant.aspx"
| stats count by App, eolcountry
```
