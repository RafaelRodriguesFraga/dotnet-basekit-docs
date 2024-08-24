---
title: Infra.MongoDb Layer
label: Infra.MongoDb
order: 6;
---

## Overview

The `DotnetBaseKit.Components.Infra.MongoDb` is a part of the DotnetBaseKit architecture, designed to facilitate data management within MongoDB domains. It provides essential configurations and utilities for interacting with MongoDB databases, aiming to streamline database operations and maintain consistency across MongoDB-related functionalities.

# Installation

Install this package via dotnet CLI or Package Manager Console:

+++ dotnet CLI
```
dotnet add package DotnetBaseKit.Components.Infra.MongoDb
```
+++ Package Manager Console
```
Install-Package DotnetBaseKit.Components.Infra.MongoDb
```
+++

Now, you have to add the dependency that contains write and read repositories. Feel free
to choose either the `Program.cs` approach or `Startup.cs` approach.

+++ Program.cs
```csharp #
var builder = WebApplication.CreateBuilder(args);
var configuration = builder.Configuration;

builder.Services.AddMongoDb(Configuration);

```
+++ Startup.cs
```csharp #
// Put this inside your ConfigureServices method
services.AddMongoDb(Configuration);
```
+++

## Usage

The primary purpose is to manage MongoDB and provide access to the database. Developers can configure MongoDB connections and perform database operations with the `IMongoSettings` interface and `MongoSettings` class. To see the configuration, go to [MongoDB Configuration](../configuration/mongodb-database-config).

With the database configured, you can use the `Infra.MongoDb` component. 

Just like the `Infra.Sql`, create a Write/Read Repository class:

```csharp #
using DotnetBaseKit.Components.Infra.MongoDb.DbSettings;
using DotnetBaseKit.Components.Infra.MongoDb.Repositories.Base;
using TestApi.Domain.Entities;
using TestApi.Domain.Repositories;

namespace YourNamespace.Infra
{
    public class YourWriteRepository : BaseWriteRepository<YourEntity>, IYourWriteRepository
    {
        public YourWriteRepository(IMongoSettings settings) : base(settings)
        {
        }
    }
}
```

```csharp #
using DotnetBaseKit.Components.Infra.MongoDb.DbSettings;
using DotnetBaseKit.Components.Infra.MongoDb.Repositories.Base;
using TestApi.Domain.Entities;
using TestApi.Domain.Repositories;

namespace YourNamespace.Infra
{
    public class YourReadRepository : BaseReadRepository<YourEntity>, IYourReadRepository
    {
        public YourReadRepository(IMongoSettings settings) : base(settings)
        {
        }
    }
}
```

Just like `Infra.Sql` you have to define an entity class that inherits from `BaseEntity`. Also you have to define an interface that extends `IBaseWriteRepository`/ `IBaseReadRepository` from the Domain Layer.

## Usage in Dependency Injection

To use the your repository in your application, register it in the dependency injection container. This ensures that the repository can be injected into services or controllers as needed.

```csharp #
using Microsoft.Extensions.DependencyInjection;
using YourNamespace.Domain.Repositories;
using YourNamespace.Infra;

namespace YourNamespace
{
    public static class ServiceExtensions
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

By following the structure provided, developers can effectively utilize the Infra.MongoDb layer to manage data access in MongoDb, ensuring consistency and maintainability across their applications.


