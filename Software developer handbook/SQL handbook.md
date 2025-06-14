[[SQL Queries box - EOL]]
**Rule of SQL:** **Normalization**

**Semi-structured data**
- JSON
- XML, HTML
- Logfile
- They are human-readable, in text form, does not follow pre-defined schema (no column)

**NoSQL** (not only SQL)
- Redis (Key-Value database)
- MongoDB (Document-based database)

**Common Table Expression**
- Put sub-query in memory
- It resolves performance issue when developer want to store sub-query in `temp_db`(hard disk)
# Basic Query

**char vs varchar**
- Fixed storage length for `char`, dynamic for `varchar`
- Example `char`: `id, language_code, phone_no, invoice_no`
- Example `varchar`: `name, description, address, profile_bio`

**Data Filtering vs Aggregation Filtering**
- `where` is data filtering
- `having` is aggregation filtering, must called after `group by`

```sql
SELECT Category, SUM(Revenue) AS TotalRevenue
FROM Sales
GROUP BY Category
HAVING SUM(Revenue) > 10000;
```

**Query Value in Range**
- use `between`

```sql
SELECT * FROM Sales
WHERE invoiceDate BETWEEN '05/31/2024' AND '08/31/2024'
```


## Ranking
- `RANK` & `DENSE_RANK`
- `ROW_NUMBER`
- `NTILE(pageLength)`
## Join
- Inner join
- Outer join
- Cross join (rarely used)
- Self join

### Fill factor
- use `FILL FACTOR 90` for securing read performance
- only use when `guid` and string.

## Others cool Q
- `UNION ALL` combine result rows of multiple query statement
- `EXCEPT`
- `INTERSECT`
- `TOP 10` returns first 10 rows
- `TOP 1 1` returns 1 if first row of the result come out
- `TABLESAMPLE (10 PERCENT)` returns first 10%
- `DISTINCT` eliminates NULL value
- `ISNULL` & `COALESCE`
- `SOME`, `ANY`
- `GETDATE`
- `sp_columns _TableName_` List columns of the table
- `sp_helpindex _TableName_` List indexes of the table 
- `sp_helpindexall`
- `sp_helptext _Programibility/Stored Procedure_` Get SQL function / Stored procedure 

---
# MS SQL Studio
- View: if you repeat same SELECT query everyday, create a view for saving time

## Dynamic Management View

**View the file size used by a database**
```sql
use eol_db
go
select * from sys.dm_db_file_space_usage
```

**View connections established in the SQL server instance**
```sql
select * from sys.dm_exec_connections
```

**View indexes usage**
To see if any index defined but does not useful
```sql
select * from sys.dm_db_index_usage_stats
```

