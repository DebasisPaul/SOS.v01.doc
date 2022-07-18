*Create Cart Entities*
- [get (C# Reference)](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/get)
- [set (C# Reference)](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/set)
- [init (C# Reference)](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/init)
- [namespace](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/namespace)
- [class (C# Reference)](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/class)
- [Introduction to classes](https://docs.microsoft.com/en-us/dotnet/csharp/fundamentals/types/classes)
- [=> operator (C# reference)](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/lambda-operator)
- [Members (C# Programming Guide)](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/members)
- [15 Structs](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/language-specification/structs)
- [Properties (C# Programming Guide)](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/properties)
- [Indexers (C# Programming Guide)](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/indexers/)
- [interface (C# Reference)](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/interface)
- [static (C# Reference)](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/static)


*Create appsettings.json*
- [Connection Strings](https://docs.microsoft.com/en-us/ef/core/miscellaneous/connection-strings)
- [Logging in .NET Core and ASP.NET Core](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/logging/?view=aspnetcore-6.0)
- [  "AllowedHosts": "*"](https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.hostfiltering.hostfilteringoptions.allowedhosts?view=aspnetcore-6.0)

*project file .csproj*
- [Understanding the project file](https://docs.microsoft.com/en-us/aspnet/web-forms/overview/deployment/web-deployment-in-the-enterprise/understanding-the-project-file)
- [.NET project SDKs](https://docs.microsoft.com/en-us/dotnet/core/project-sdk/overview)
- [Configuration in ASP.NET Core](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/configuration/?view=aspnetcore-6.0)

*shopOnlineDbContext.cs*

```
public class ShopOnlineDbContext:DbContext
    {
        public ShopOnlineDbContext(DbContextOptions<ShopOnlineDbContext> options):base(options)
        {
            
        }
```
- [DbContext Class](https://docs.microsoft.com/en-us/dotnet/api/microsoft.entityframeworkcore.dbcontext?view=efcore-6.0 https://docs.microsoft.com/en-us/dotnet/api/system.data.entity.dbcontext?view=entity-framework-6.2.0)
- [DbContext Lifetime, Configuration, and Initialization](https://docs.microsoft.com/en-us/ef/core/dbcontext-configuration/)
- [Working with DbContext](https://docs.microsoft.com/en-us/ef/ef6/fundamentals/working-with-dbcontext)

```
 protected override void OnModelCreating(ModelBuilder modelBuilder)
        {
            base.OnModelCreating(modelBuilder);
```
- [DbContext.OnModelCreating(ModelBuilder) Method](https://docs.microsoft.com/en-us/dotnet/api/microsoft.entityframeworkcore.dbcontext.onmodelcreating?view=efcore-6.0)
- [DbContext.OnModelCreating(DbModelBuilder) Method](https://docs.microsoft.com/en-us/dotnet/api/system.data.entity.dbcontext.onmodelcreating?view=entity-framework-6.2.0)
- [Creating and configuring a model](https://docs.microsoft.com/en-us/ef/core/modeling/)
- [Inheritance](https://docs.microsoft.com/en-us/ef/core/modeling/inheritance)
- [Entity Properties](https://docs.microsoft.com/en-us/ef/core/modeling/entity-properties?tabs=data-annotations%2Cwithout-nrt)

```
         modelBuilder.Entity<Product>().HasData(new Product
            {
                Id = 1,
                Name = "Glossier - Beauty Kit",
                Description = "A kit provided by Glossier, containing skin care, hair care and makeup products",
                ImageURL = "/Images/Beauty/Beauty1.png",
                Price = 100,
                Qty = 100,
                CategoryId = 1

            });
```

- [EntityTypeBuilder<TEntity>.HasData Method](https://docs.microsoft.com/en-us/dotnet/api/microsoft.entityframeworkcore.metadata.builders.entitytypebuilder-1.hasdata?view=efcore-6.0)
  [EntityTypeBuilder.HasData Method](https://docs.microsoft.com/en-us/dotnet/api/microsoft.entityframeworkcore.metadata.builders.entitytypebuilder.hasdata?view=efcore-6.0)
  
  ```
        public DbSet<Cart> Carts { get; set; }
        public DbSet<CartItem> CartItems { get; set; }
        public DbSet<Product> Products { get; set; }
        public DbSet<ProductCategory> ProductCategories { get; set; }
        public DbSet<User> Users { get; set; }
  ```
  - [Defining DbSets](https://docs.microsoft.com/en-us/ef/ef6/modeling/code-first/dbsets)
  [DbSet Class](https://docs.microsoft.com/en-us/dotnet/api/system.data.entity.dbset?view=entity-framework-6.2.0)
  [DbSet<TEntity> Class](https://docs.microsoft.com/en-us/dotnet/api/system.data.entity.dbset-1?view=entity-framework-6.2.0)
    
    ```
    builder.Services.AddDbContextPool<ShopOnlineDbContext>(options =>
    options.UseSqlServer(builder.Configuration.GetConnectionString("ShopOnlineConnection"))
);
    ```
   
    - [Part 5, work with a database in an ASP.NET Core MVC app](https://docs.microsoft.com/en-us/aspnet/core/tutorials/first-mvc-app/working-with-sql?view=aspnetcore-6.0&tabs=visual-studio)
    - [EntityFrameworkServiceCollectionExtensions.AddDbContextPool Method](https://docs.microsoft.com/en-us/dotnet/api/microsoft.extensions.dependencyinjection.entityframeworkservicecollectionextensions.adddbcontextpool?view=efcore-6.0)
    [SqlServerDbContextOptionsExtensions.UseSqlServer Method](https://docs.microsoft.com/en-us/dotnet/api/microsoft.entityframeworkcore.sqlserverdbcontextoptionsextensions.usesqlserver?view=efcore-6.0)
    [Configuration Class](https://docs.microsoft.com/en-us/dotnet/api/system.configuration.configuration?view=dotnet-plat-ext-6.0)
    [Connection Strings](https://docs.microsoft.com/en-us/ef/core/miscellaneous/connection-strings)
    
*Migration*
    - [Migration.Down(MigrationBuilder) Method](https://docs.microsoft.com/en-us/dotnet/api/microsoft.entityframeworkcore.migrations.migration.down?view=efcore-6.0)
    - [https://docs.microsoft.com/en-us/dotnet/api/microsoft.entityframeworkcore.migrations.migration.down?view=efcore-6.0](https://docs.microsoft.com/en-us/dotnet/api/microsoft.entityframeworkcore.migrations.migrationbuilder.droptable?view=efcore-6.0)
   - [MigrationBuilder.InsertData Method](https://docs.microsoft.com/en-us/dotnet/api/microsoft.entityframeworkcore.migrations.migrationbuilder.insertdata?view=efcore-6.0)
- [MigrationBuilder.CreateTable Method](https://docs.microsoft.com/en-us/dotnet/api/microsoft.entityframeworkcore.migrations.migrationbuilder.createtable?view=efcore-6.0)
- [Migration.Up(MigrationBuilder) Method](https://docs.microsoft.com/en-us/dotnet/api/microsoft.entityframeworkcore.migrations.migration.up?view=efcore-6.0)
    
