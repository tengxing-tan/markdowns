> Used to get last page URL for back button

Two options: 
- `Request.UrlReferrer`, General method, not suitable if navigate from `cshtml` to `aspx`
- `lastReferrer`, exactonline method, it is stable and can be expected

```vb
btnClose.navigateURL = ClosePageUrl().ToString

Private Function ClosePageUrl() As UrlBuilder

	Return New UrlBuilder(LastReferrer, env.EnvironmentByType)

	Return New UrlBuilder(Request.UrlReferrer, env.EnvironmentByType)
End Function
```
