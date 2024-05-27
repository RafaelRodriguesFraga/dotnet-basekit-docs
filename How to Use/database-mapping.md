---
title: Database Mapping / Config
label: Database Mapping / Config
order: 4;
---

There are many ways to perform database mapping in .NET. In Dotnet Basekit, the Fluent API approach is used, with database mapping configurations located in the Infra layer.

```csharp #
using YourNamespace.Domain.Entities;
using Microsoft.EntityFrameworkCore;
using Microsoft.EntityFrameworkCore.Metadata.Builders;

namespace YourNamespace.Infra.Configurations
{
    public class YourEntityConfiguration : IEntityTypeConfiguration<YourEntity>
    {
        public void Configure(EntityTypeBuilder<YourEntity> builder)
        {
            builder.Ignore(entity => entity.Notifications);
            builder.Ignore(entity => entity.Valid);
            builder.Ignore(entity => entity.Invalid);

            builder.ToTable("your_database");
            builder.HasKey(x => x.Id);

            builder.Property(x => x.Id)
                .IsRequired()            
                .HasColumnName("id");

            builder.Property(x => x.CreatedAt)
                .IsRequired()
                .HasColumnType("timestamp without time zone")
                .HasColumnName("created_at");

            builder.Property(x => x.Field1)
                .HasMaxLength(100)
                .IsRequired()
                .HasColumnName("credit_card_name");

            builder.Property(x => x.Field2)                
                .IsRequired()
                .HasColumnName("field_1");
        }
    }
}
```

When mapping an entity to a database, if you do not specify a column name for your entity attributes or table, EF Core will default to using double quotes around the names during migration. For example:
You choose an `Entity` to map to a database. If you dont choose a column name for your entities attributes or table, EF Core after execute a migration will put the name in double quotes. It would be like this:

```sql
select "Field1" from "your_table"
```

To avoid this, explicitly choose names for your columns and tables, as demonstrated above.
## Important Notes

   **1. Ignored Properties:** In this version of BaseKit, you must ignore the properties `Notifications`, `Invalid`, and `Valid` in every entity to prevent errors. This will be fixed in future updates.

   **2. Naming Recommendations:** We recommend using lowercase and snake_case for your fields, especially `id` and `created_at` (inherited from BaseEntity).
 
## Explanation

In this version of the BaseKit you have to ignore these first three properties in every single entity (`Notifications`, Invalid` and `Valid`) or otherwise will throw an error. This will be fixed soon.

The other thing is that we recommend in this version to put your fields in lowercase and snake_case, mainly `id` and `created_at` (they come from `BaseEntity`).

## FluentAPI Methods

- To make a field required, use the `IsRequired()` method.
- To specify a column name, use the `HasColumnName(<name>)` method.
- To set a maximum length for a field, use the `HasMaxLength(<number>)` method.
- To define a column type, use the `HasColumnType(<type>)` method.
- To specify a table name, use the `ToTable(<table_name>)` method.

To see more of FluentAPI, see the official docummentation [here](https://learn.microsoft.com/pt-br/ef/ef6/modeling/code-first/fluent/types-and-properties);

## Using your Mapping

After configuring all of the fields, you can use your mapping in the `OnModelCreating()` method in your `DbContext`:

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

            // Put your configurations here
            modelBuilder.ApplyConfiguration(new YourEntityConfiguration());

        }
    }
}
```

**Note:** Some people refer to database mapping as `Configuration`, while others call it `Map`. In this example, we use the term `Configuration`. Feel free to use the term that you like.
