
> [!INFO]  Info
> - Read Software engineer handbook for quick recap.
> - Open command palette; ***Show outline***

# Format
- Unnecessary comments & libraries must be removed.
- Main flow first, then helper.
```js
// properties
const ingredients = [];
const kitchenTools = [];
// Main
function cook() {
	prepareIngredient()
	setupKitchen()
	fire()
}
// Helper
function prepareIngredient() {}
function setupKitchen() {}
function fire() {}
```

---

# Best practice
## Class properties
```cs
// Starts with underscore: class properties
private readonly int _successCount;
// variable
int successCount
```

---

# Performance
## SQL should not in for loop
- Sending one query = travel from web server to firewall to load balancer to database.
- Get all result in one query, then use `.Where()` to get intended result.
```cs
// Expensive
foreach(var item in list)
{
	DataModel sqlResult = store.Get();
}
// Affortable
List<DataModel> sqlResult = store.Get();
foreach(DataModel item in sqlResult)
{
	// No sql querying, only have business logic
}
```

## Lazy initialization

- If two queries/initializations are returning same thing, then store in class properties to reuse.
- Code snippet: [[Lazy initialization]]

---

# Security
## Encode HTML
```cs
// Bad
Paragraph.Value = Text.Replace(vbCrLf, "<br />")
// Good
Paragraph.Value = Tools.HtmlEncodeLines(Text)
```

---

# Maintainability
## Break down crowded function
```vb
Sub Page_Init() 
	'Good
	GetMessage();
	SetErrorMessage();
	SetLength();
	'Bad
	if () Then
		'crowded logic & nested if
End Sub
```

## Write descriptive assert message
Explain why it is incorrect.
```cs
// Bad
Assert.AreEqual(expected, actual, "Actual result is not 01/05/2024");
// Good
Assert.AreEqual(expected, actual, "VariableName should be 01/05/2024");
```

## Write descriptive function name

```cs
// Bad
Copy_WhenDossierContainsSameDocumentType_ThenShowError()
Copy_WhenDossierContainsSameDocumentTypeInMultipleFolders_ThenShowDossierFoldersInError()
// Good
Copy_DossierHas1FolderContainsSameDocumentTypes_SkipCopyAndReturnsErrorResult()
Copy_DossierHas2FoldersContainSameDocumentTypes_SkipCopyAndReturnsErrorResult()```
**Explaining**
- no `Multiple`, use `1` and `2`, ***be concise***.
- `SkipCopy`: ***acceptance criteria***.
- no `When`, `Then`, ***redundant***.
- no `Show`, only `Returns`, this is ***backend*** not frontend. 

## SOLID Principles
- [SOLID Principles (freecodecamp)](https://www.freecodecamp.org/news/solid-principles-for-programming-and-software-design/)

### Dependency Inversion Principle
- High level does not import low level methods, they both depend to abstraction (i.e. interface).
- Abstract independent of detail. Detail dependent of abstract.
```js
// Bad
const filter = new Kendo.filter(params); // app.js

// Good 
function initFilter(params) {  // filter.js
	return new Kendo.filter(params);
}
filter = initFilter(params); // app.js
```


---


