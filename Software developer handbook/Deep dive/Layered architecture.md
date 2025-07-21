3 layers
1. Core
	1. fundamental logic: CRUD
	2. simple & stupid. no permission checking
	3. reusability
2. Services
	1. handle specific business logic
	2. validation, authentication, permission checking are done here
	3. scalability, can be grow without affecting core & web layers
3. Web
	1. API call: GET, POST, PUT, DELETE done here
	2. user interaction