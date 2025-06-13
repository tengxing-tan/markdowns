**Problem:**
- No activity shown in plan board
- But everything is setup properly, yet already set activities

## Troubleshoot
- Check is background task running

**Check PM background task**
- Go to `Hosting > Hosting Setup > Baskground task > On demand background task`
- Search for PM related background task
- These should be waiting

## Solution
**Run this SQL on each database**
- Change line 2 to your computer code
```sql
IF NOT EXISTS(SELECT * FROM sys.database_principals WHERE name = 'EOLBackground')
    CREATE USER [EOLBackground] FOR LOGIN [LT-24-507\EOLBackground] WITH DEFAULT_SCHEMA=[dbo]
ALTER ROLE [db_datareader] ADD MEMBER [EOLBackground]
ALTER ROLE [db_datawriter] ADD MEMBER [EOLBackground]
ALTER ROLE [EOLLogger] ADD MEMBER [EOLBackground]
ALTER ROLE [EOLUser] ADD MEMBER [EOLBackground]
IF dbo.DatabaseType() = 'Conversion'
    ALTER ROLE [EOLCreator] ADD MEMBER [EOLBackground]
```

