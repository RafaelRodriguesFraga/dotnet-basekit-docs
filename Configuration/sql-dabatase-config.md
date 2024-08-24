---
title: SQL Database Configuration
label: SQL Database Config
order: 1;
---

## SQL Database Configuration

The following `appsettings.json` sample includes all possible [configuration](../full-appsettings-config) options.

[!file appsettings.json](../static/appsettings.json)

After creating your Database Context ([see here](../components/infra-sql/#usage)) and mapping your database using Fluent API [here](../how-to-use/database-mapping), you can configure your appsettings.json as follows to support multiple databases:

```json
{
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft.AspNetCore": "Warning"
    }
  },
  "SelectedDatabase": "Postgres | MySql | SqlServer",  // Can be "Postgres", "MySql", or "SqlServer"
  "ConnectionStrings": {
    "PostgresConnection": "Host=localhost;Port=5432;Database=your_database;Username=your_database;Password=postgres;",
    "MySqlConnection": "Server=localhost;Database=your_database;User=your_user;Password=your_user;",
    "SqlServerConnection": "Server=localhost;Database=test;User Id=sa;Password=your_password;"
  },
  "AllowedHosts": "*"
}
```

### Detailed Configuration

DotnetBaseKit offers support for PostgreSQL, MySQL, and SQL Server in this version. You can choose any of these databases by setting the `SelectedDatabase` property to Postgres, MySql, or SqlServer. Each database has its own connection string property as described below:

### PostgreSQL Configuration

To use PostgreSQL, set `SelectedDatabase` to Postgres and provide the connection details under PostgresConnection.

```json #
{
  "SelectedDatabase": "Postgres",
  "ConnectionStrings": {
    "PostgresConnection": "Host=localhost;Port=5432;Database=your_database;Username=your_username;Password=your_password;"
  }
}
```

### MySQL Configuration

To use MySQL, set `SelectedDatabase` to MySql and provide the connection details under MySqlConnection.

```json #
{
  "SelectedDatabase": "MySql",
  "ConnectionStrings": {
    "MySqlConnection": "Server=localhost;Database=your_database;User=your_user;Password=your_password;"
  }
}
```

### SQL Server Configuration

To use SQL Server, set `SelectedDatabase` to SqlServer and provide the connection details under SqlServerConnection.

```json #
{
  "SelectedDatabase": "SqlServer",
  "ConnectionStrings": {
    "SqlServerConnection": "Server=localhost;Database=your_database;User Id=your_user;Password=your_password;"
  }
}
```

You can switch between the databases by changing the value of `SelectedDatabase` to either Postgres, MySql, or SqlServer as needed. Each setting will ensure that the correct connection string is used for your selected database.
