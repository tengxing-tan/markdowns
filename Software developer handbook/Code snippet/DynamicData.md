Available on C# and .NET framework
```cs
[DataTestMethod]
[DynamicData(nameof(GetTestData), DynamicDataSourceType.Method)]
public void SearchCreditor_DataDriven_Test2(
	string testcaseId, string existingAccountName, string newAccountName, string remarks, bool find)
{
	var existingAccountId = CreateCreditor(existingAccountName);

	if (find)
	{
		TestFound(testcaseId, existingAccountId, existingAccountName, newAccountName, remarks);
	}
	else
	{
		TestNotFound(testcaseId, existingAccountId, existingAccountName, newAccountName, remarks);
	}
	Context.AssertEmptyErrorLog();
}

private static IEnumerable<object[]> GetTestData()
{
	yield return new object[] { "0", "Albert Heijn", "Albert Heijn", "Identical", true };
	yield return new object[] { "1", "Albert Heijn", "albert heijn", "Different casing", true };
	yield return new object[] { "2", "Albert Heijn", "Albert  Heijn", "Difference in spaces", true };
	yield return new object[] { "3", "Albert Heijn", "Albert-Heijn", "Difference in separation characters", true };
	yield return new object[] { "4", "Albert Heijn", "Albért Heijn", "Difference in accents (special characters)", true };
}
```