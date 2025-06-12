```cs
[DataTestMethod, XmlDataSource(@"TestData\SqlAnalyzerNormalize.xml", "SqlAnalyzerNormalize")]
public void Normalize(string normalized, string sql)
{
	// Act
	var result = SqlAnalyzer.Normalize(sql);

	// Assert
	Assert.AreEqual(normalized, result.ToString());
}
```