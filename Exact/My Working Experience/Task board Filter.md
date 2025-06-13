# Import Javascript in aspx and aspx.vb

> This is .NET framework

**Code behind, aspx.vb**
It renders another JavaScript named `AccPracticeServiceDeliverableCard`.

```
Protected Sub RenderScript_RenderEvent(output As HtmlTextWriter)
	RenderScriptResource(output, "AccPracticeServiceDeliverableCard")
End Sub
```

**aspx**
```aspx
<ex:RenderPlaceholder ID="RenderScript" runat="server" OnRenderEvent="RenderScript_RenderEvent" />
```

Done importing JavaScript. Use the js function like: 

**same aspx file here**, and I called `CloseScreen()` function.
```aspx
<ex:Button runat="server" ID="btnClose" ButtonStyle="Close" Caption="Close" CaptionID="8450" OnClick="CloseScreen();" />
```

> `CloseScreen()` is located in `Sources/content/AccPracticeServiceDeliverableCard.js`
