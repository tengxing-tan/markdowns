```sql
CREATE LOGIN [IIS APPPOOL\DefaultAppPool] FROM WINDOWS
CREATE LOGIN [IIS APPPOOL\.NET v4.5] FROM WINDOWS
CREATE LOGIN [LT-24-528\EOLBackground] FROM WINDOWS
--CREATE LOGIN [ecs\TANT441323] FROM WINDOWS -- User ID, eg: john123456
 
ALTER SERVER ROLE dbcreator ADD MEMBER [LT-24-528\EOLBackground]
ALTER SERVER ROLE sysadmin  ADD MEMBER [ecs\TANT441323] -- User ID, eg: john123456
ALTER SERVER ROLE sysadmin  ADD MEMBER [IIS APPPOOL\DefaultAppPool]
```

**Create a new service for another `exactonline` repo**
```cmd
sc create ExactBGService_eol_custom_name binpath=C:\Repos\temp-exactonline\WebApp\Sources\bin\Exact.BGTasks.service.exe
```

**Create logon/reuse existing user account**
1. Computer Management > Local Users & Groups > Users > Create new User
2. Make sure password never expired ✅
3. Then open MSSQL, grant permission to the service.

```sql
CREATE LOGIN [LT-24-528\ExactBGService_eol_custom_name] FROM WINDOWS
ALTER SERVER ROLE dbcreator ADD MEMBER [LT-24-528\ExactBGService_eol_custom_name]
```