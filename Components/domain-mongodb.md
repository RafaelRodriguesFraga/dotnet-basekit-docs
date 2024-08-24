---
title: Domain.MongoDb Layer
label: Domain.MongoDb
order: 4;
---

## Overview

The `DotnetBaseKit.Components.Domain.MongoDb` part of the DotnetBaseKit architecture, designed to facilitate data management within MongoDb. It offers foundational structures for entities, DTOs, and repositories, aiming to streamline database interactions and maintain consistency across MongoDb functionalities. By adhering to the principles of separation of concerns and repository pattern, this layer promotes code organization, and reusability in MongoDb operations within the application's domain.

# Installation

Install this package via dotnet CLI or Package Manager Console:

+++ dotnet CLI
```
dotnet add package DotnetBaseKit.Components.Domain.MongoDb
```
+++ Package Manager Console
```
Install-Package DotnetBaseKit.Components.Domain.MongoDb
```
+++

## Usage

The primary purpose of the `BaseEntity` and `BaseDto` classes is to serve as foundational structures for entities and DTOs within the MongoDb domain of the application. By inheriting from these classes, developers can benefit from their validation and notification handling capabilities, ensuring a consistent approach to managing entities and DTOs across MongoDb-related functionalities.

For example, consider a scenario where we have an entity named Product representing products in an e-commerce application. We can define the Product entity as follows:

```csharp #
using DotnetBaseKit.Components.Domain.MongoDb.Entities.Base;

namespace YourNamespace.Entities
{
    public class Product : BaseEntity
    {
        // constructors

        public string Name { get; private set; } = string.Empty;
        public decimal Price { get; private set; } = string.Empty;

        public override void Validate()
        {
            // Custom validation logic for the Product entity
            // See more on the link below
            
        }
    }
}
```

In this example, the `Product` class inherits from `BaseEntity` and implements its `Validate()` method to perform custom validation logic specific to the Product.

Similarly, consider a DTO named `ProductDto` representing product data transferred between layers of the application. We can define the ProductDto class as follows:

```csharp #
using DotnetBaseKit.Components.Domain.MongoDb.Dtos.Base;

namespace YourNamespace.Dtos
{
    public class ProductDto : BaseDto
    {
        public string Name { get; set; } = string.Empty;
        public decimal Price { get; set; } = string.Empty;

        public override void Validate()
        {
            // Custom validation logic for the Product entity
            // See more on the link below
        }
    }
}
```

In this example, the `ProductDto` class inherits from BaseDto and implements its `Validate()` method to perform custom validation logic specific to the `ProductDto`.

By utilizing the `BaseEntity` and `BaseDto` classes in this manner, developers can ensure consistent validation and notification handling within the MongoDb domain of the application.

[!ref Go to Validations](/how-to-use/validations)

## Repository Pattern

The `DotnetBaseKit.Components.Domain.MongoDb` also provides interfaces for read and write repositories, `IBaseReadRepository` and `IBaseWriteRepository`. These interfaces define the methods required for data access operations, adhering to the repository pattern. This pattern helps in encapsulating the data access logic and promotes a cleaner separation of concerns for MongoDb.

Create a Write / Read Repository Interface:

```csharp # 
using DotnetBaseKit.Components.Domain.MongoDb.Repositories.Base;
using YourNamespace.Domain.Entities;

namespace YourNamespace.Domain.Repositories
{
    public interface IYourRepositoryWriteRepository : IBaseWriteRepository<YourEntity>
    {
    }
}
```

```csharp # 
using DotnetBaseKit.Components.Domain.MongoDb.Repositories.Base;
using YourNamespace.Domain.Entities;

namespace YourNamespace.Domain.Repositories
{
    public interface IYourRepositoryWriteRepository : IBaseWriteRepository<YourEntity>
    {
    }
}
```

PS: Do not confuse `IBaseWriteRepository` from `Domain.Sql` with `IBaseWriteRepository` from `Domain.MongoDb`. `IBaseWriteRepository` from `Domain.Sql`  is from `DotnetBaseKit.Components.Domain.Sql.Repositories.Base`namespace and `IBaseWriteRepository` from `Domain.MongoDb` is from `DotnetBaseKit.Components.Domain.MongoDb.Repositories.Base` namespace. In future releases this will be fixed too for clear understanding. 

You can see the fully usage of the repository in [Infra.MongoDb](../infra-MongoDb/#usage) or in the [Fully Usage Example for MongoDb](../../how-to-use/fully-example-MongoDb)
