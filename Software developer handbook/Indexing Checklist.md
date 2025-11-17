Here’s a **checklist of indicators for when to create an index** in SQL Server (or most relational databases):

***

### ✅ **Column Characteristics**

1.  **High Selectivity**
    *   Many distinct values compared to total rows (low `All density` in `DBCC SHOW_STATISTICS`).
    *   Example: `CustomerID`, `Email`.

2.  **Frequently Used in WHERE Clauses**
    *   Columns often appear in filters or search conditions.

3.  **Used in JOIN Conditions**
    *   Columns that connect tables (foreign keys, primary keys).

4.  **Used in ORDER BY or GROUP BY**
    *   Sorting and grouping benefit from indexes.

5.  **Used in Aggregate Functions with Filters**
    *   Example: `COUNT(*) WHERE status = 'Active'`.

***

### ✅ **Query Patterns**

6.  **High Read-to-Write Ratio**
    *   Tables that are read often but updated less frequently.

7.  **Large Table Size**
    *   Indexing small tables rarely helps; large tables benefit more.

8.  **Frequent Range Queries**
    *   Example: `WHERE date BETWEEN '2025-01-01' AND '2025-11-01'`.

***

### ✅ **Performance Indicators**

9.  **Slow Query Execution**
    *   Queries doing full table scans instead of index seeks.

10. **High I/O or CPU Usage**
    *   Check execution plans for scans instead of seeks.

***

### ✅ **Avoid Indexing When**

*   Column has **low selectivity** (e.g., `Gender`, `IsActive`).
*   Table is **small** (index overhead > benefit).
*   Column is **frequently updated** (indexes slow down writes).

***

