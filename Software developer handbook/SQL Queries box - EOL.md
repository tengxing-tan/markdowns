**Get user/isAccountant/etc**
```sql
--this query get users with details: Division, username, full namae, id
use eol
go
select distinct Divisions.Code as Division, Users.UserName, users.FullName, accounts.id from Users
	left join Accounts on Users.Customer = Accounts.ID 
	left join divisions on Divisions.Customer = Users.Customer
	left join CustomerFeatureSets on Users.Customer = CustomerFeatureSets.Customer
	left join FeatureSets on FeatureSets.id = CustomerFeatureSets.FeatureSet
	where UserName like 'customer%'
	order by users.FullName

```


