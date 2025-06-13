Keep an eye on file location, virtual path, database name. 
```cmd
net stop "ExactBGService"
iisreset /stop

cd C:\Repos\exactonline\Build
powershell -F clean-build.ps1

cd C:\Repos\exactonline
powershell Deploy\deploy-local-development.ps1 -VirDir 'dev' -HostingDbName 'Eol'

cd .\WebApp\Sources
.\bin\Exact.DatabaseUpdater.exe /HOSTINGLOC:x

net start "ExactBGService"
iisreset /start
```

**Recommend virtual directory**
http://localhost/EOL
http://localhost/dev
http://localbost/EOLDev
http://localhost/EOLRelease 
http://localhost/EOLMaster

## Troubleshoot

**Error Message: Access denied**
```plain
Program 'System.Configuration.ConfigurationManager.dll' failed to run: No application is associated with the specified file for this operationAt line:1 char:1
```

- Stop background task
- Done!

**OWIN startup**
```text
For the app startup parameter value 'Exact.Online.Web.ExactOnlineStartup, Exact.Online.Web', the assembly 'Exact.Online.Web' was not found.
```

- `Exact.Onlin.Web` built failed, check last commit or build in Visual Studio to see the error.  