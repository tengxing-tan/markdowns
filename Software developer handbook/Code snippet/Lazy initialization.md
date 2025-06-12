3 steps:
- Declaration & initialization
- Deferred function
- Caching

```cs
public class Class
{
	// declaration
	private Lazy<int> Count;

	public Class()
	{
		// initialization
		Count = new Lazy<int>(() => Store.GetCount()) 
		// Deferred: Store.GetCount()
		// action or computation is postponed until later time
	}

	private int GetCount()
	{
		// Once first invoke, value has cached
		return Count; 	
	}
}
```