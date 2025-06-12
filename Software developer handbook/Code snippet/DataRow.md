Available on C# and .NET framework
```cs
[DataTestMethod]
[DataRow(1, "App", "App", "Identical", true)]
[DataRow(2, "App", "app", "Different casing", true)]
[DataRow(3, "App", "A pp", "Difference in spaces", true)]
public void SearchCreditor_DataDriven_Test2(
	int scenario, string left, string right, string remarks, bool isApp)
{
	// Integration & Unit test: Arrange, Act, Assert
}
```