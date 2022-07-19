*Technologies*
- Visual Studio 2022
- .Net 7
- SQL Server 2022
- Blazor WebAssembly
- Botstrap v5
- Restful MVC Web API (for database related functionality and returning relavent data from the server to our client side Blazor Application)
- Payment Gateway Integration

*Project Workfow*

*Part1*
- Create ShopOnline.Web Blazor Web Aseembly App
- Create ShopOnline.Api ASP.NET Core Web API 
- Create Entities Folder // this is where the classes will represent our database entities will resides.
- install Microsoft.EntityFrameworkCore.SQLServer
- install Microsoft.EntittyFrameworkCore.Tools
- Configure Connection String in appsetting.json
- Create ShopOnlineContext Class
- Seed Database by override OnModelCreating method
- Create Entity framework core DBSet generic Type
- Register ShopOnlineDbContext class for Dependency Injection

*Part2*

- Retrieving Product data from our database & returning the data to the client blazor component.
- Create DTO Model, dto is an objetc that defines how the data will be send over the network.
- Create Class Library project
- Using Repository Design Pattern To Abstract our data handling layout. Repositories are classes or component that encapsulate the logic required to access data sources.
- Create Repositories folder
