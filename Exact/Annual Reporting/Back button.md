# Key findings
- `menu.component.ts` invoked `updateNavigation(groupNavigationItems)`
- update current item group if true: `this.setItemGroup`
- emit event data, in the `<fg-document-base>`, property of `<fg-menu>`, `(currentItemGroupChanged)="onItemGroupChanged($event)`"
- once emitted, `currentItemGroup` in both `<fg-document-base>` & `<fg-navigator>` will be updated
- How to supply `groupNavigationItems`? 
	- In `document-base html`, property of `<fg-menu>` `[navigation]="documentPage.currentSheet.navigationItems"`
- `documentPage`? 
	- get idea from `document.model.ts`
	- Same thing in MVC: `DocumentViewModel.cs`
- how to supply `documentPage`
	- in `document-base.component.ts`, 
		- `const document = this.activatedRoute.snapshot.data['data'];`
- how to get `currentGroupItem` set value
	- `ItemGroupNavigator.cs` ``
	- 
`
