

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