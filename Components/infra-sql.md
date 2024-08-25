---
title: Infra.Sql Layer
label: Infra.Sql
order: 5;
---

## Overview

The `DotnetBaseKit.Components.Infra.Sql` layer is a crucial part of the DotnetBaseKit architecture, designed to handle the data access logic for SQL databases. It provides a base context for Entity Framework Core, along with repository implementations for standard CRUD operations. This layer promotes the separation of concerns by encapsulating data access logic and offering reusable components for managing SQL database interactions.

## Installation

Install this package via dotnet CLI or Package Manager Console:

+++ dotnet CLI
```
dotnet add package DotnetBaseKit.Components.Infra.Sql
```
+++ Package Manager Console
```
Install-Package DotnetBaseKit.Components.Infra.Sql
```
+++

Now, you have to add the dependency that contains write and read repositories. Feel free
to choose either the `Program.cs` approach or `Startup.cs` approach.

+++ Program.cs
```csharp #
var builder = WebApplication.CreateBuilder(args);
var configuration = builder.Configuration;

builder.Services.AddDbContext<YourContext>(configuration);
```
+++ Startup.cs
```csharp #
// Put this inside your ConfigureServices method
services.AddDbContext<YourContext>(Configuration);
```
+++

## DbContext Base Class

The `BaseContext` class serves as a foundational DbContext for Entity Framework Core, providing basic configurations and constructors.

```csharp #
using Microsoft.EntityFrameworkCore;

namespace DotnetBaseKit.Components.Infra.Sql.Context.Base
{
    public class BaseContext : DbContext
    {
        protected BaseContext() : base() { }

        protected BaseContext(DbContextOptions options) : base(options) { }
    }
}
```

## Usage

The primary purpose of the `BaseContext` and the repository classes is to provide a standardized approach to data access in SQL databases. By utilizing these classes, developers can ensure consistent data management practices across the application.

Configure your `DbContext`: 

```csharp #
using DotnetBaseKit.Components.Infra.Sql.Context.Base;
using DotnetBaseKit.Components.Shared.Notifications;
using Microsoft.EntityFrameworkCore;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using YourNamespace.Infra.Configurations;

namespace YourNamespace.Context
{
    public class YourContext : BaseContext
    {
        public YourContext(DbContextOptions<YourContext> options) : base(options)
        {
        }

        protected override void OnModelCreating(ModelBuilder modelBuilder)
        {
            base.OnModelCreating(modelBuilder);
            modelBuilder.Ignore<Notification>();

            // Other configurations
        }
    }
}
```

You have to add `modelBuilder.Ignore<Notification>()`, otherwise it will throw an error. In future releases this will be fixed. For fully usage of the `Infra.Sql` see the [Fully Usage Example](../../how-to-use/fully-example) or [SQL Database Configuration](../configuration/sql-dabatase-config).

Create a Write/Read Repository: 

```csharp #
using DotnetBaseKit.Components.Infra.Sql.Context.Base;
using DotnetBaseKit.Components.Infra.Sql.Repositories.Base;
using YourNamespace.Domain.Entities;
using YourNamespace.Domain.Repositories;

namespace YourNamespace.Infra
{
    public class YourWriteRepository : BaseWriteRepository<YourEntity>, IYourWriteRepository
    {
        public YourWriteRepository(BaseContext context) : base(context)
        {
        }
    }
}
```

```csharp #
using DotnetBaseKit.Components.Infra.Sql.Context.Base;
using DotnetBaseKit.Components.Infra.Sql.Repositories.Base;
using YourNamespace.Domain.Entities;
using YourNamespace.Domain.Repositories;

namespace YourNamespace.Infra
{
     public class YourReadRepository : BaseReadRepository<YourEntity>, IYourReadRepository
    {
        public YourReadRepository(BaseContext context) : base(context)
        {
        }
    }
}
```

As you can see, you have to define an entity class that inherits from `BaseEntity`. Also you have to define an interface that extends `IBaseWriteRepository`/ `IBaseReadRepository` from the Domain Layer.

## Usage in Dependency Injection

To use the your repository in your application, register it in the dependency injection container. This ensures that the repository can be injected into services or controllers as needed.

```csharp #
using Microsoft.Extensions.DependencyInjection;
using YourNamespace.Domain.Repositories;
using YourNamespace.Infra;

namespace YourNamespace
{
    public static class RepositoryExtensions
    {
        public static IServiceCollection AddRepositories(this IServiceCollection services)
        {
            services.AddScoped<IYourWriteRepository, YourWriteRepository>();
            services.AddScoped<IYourReadRepository, YourReadRepository>();

            // other Repositories
            return services;
        }
    }
}
```

Register your extension method on `Program.cs` or `Startup.cs`:


+++ Program.cs
```csharp #
var builder = WebApplication.CreateBuilder(args);
var configuration = builder.Configuration;

builder.Services.AddRepositories();
```
+++ Startup.cs
```csharp #
// Put this inside your ConfigureServices method
services.AddRepositories();
```
+++

By following the structure provided, developers can effectively utilize the Infra.Sql layer to manage data access in SQL databases, ensuring consistency and maintainability across their applications.