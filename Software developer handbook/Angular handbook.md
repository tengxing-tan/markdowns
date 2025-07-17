>[!info] Info
>[[#Code review best practice]]


use route parameters to pass data to a route

- `ActivatedRoute - @angular/core` gets params from URL
- `HousingService - dev defined` manages data
```ts
// class component {
route: ActivatedRoute = inject(ActivatedRoute);
housingService = inject(HousingService);
constructor() {
    const housingLocationId = Number(this.route.snapshot.params['id']);
	this.housingLocation = this.housingService.getHousingLocationById(housingLocationId);
}
```


# Code review best practice
- Avoid not-null assertion. `assumeNotNull!: boolean;`
- Avoid async that leads memory leak when it is trying to search for destroyed component. 
	- Use `.then()`
	- or `.subscribe()`
- Use guard-clause. `if (!value) return;`
- Use strict equality `===` to compare object type as well
- Use `enum`, not hard code. `Type.One✅ 1❌`
- Use implicit type. `(result: boolean) => ()`
- Avoid custom CSS

## Angular
- Use `take(1)` or/and `takeUntil(this.ngUnsubscribe))` to ensure that resources are properly cleaned up and preventing memory leaks.