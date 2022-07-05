###  📦 Tips & Tricks
---
```
Problem:   Add-Migration InitialCreate Not Working `Could not load assembly 'ShopOnline.Web'. Ensure it is referenced by the startup project 'ShopOnline.Api'.`
Solution: `https://www.thecodebuzz.com/build-failed-efcore-scaffold-dbcontext-command-pmc/`
```
```
Problem: Add-Migration InitialCreate
Build started...
Build failed.
Solution: Open ShopOnlineDbContext.cs file Then Check the code & find the error. Two error found at UserName. Open User.cs Entities. Correct the int to string type.
```
```
[Q]  Why We Use Migrations?
[A] Migration Allow us to evolve our database without loosing data or database object.
```
```
[Q]  sorry there's nothing at this address.
[A] https://github.com/dotnet/aspnetcore/issues/20786
```
