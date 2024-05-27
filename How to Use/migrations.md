---
title: Migrations
label: Migrations
order: 5;
---

## Overview

Migrations are a way to keep the database schema in sync with the application's data model. They allow you to incrementally apply schema changes to your database, making it easier to evolve your database structure over time while preserving the data and share among developers.

## Instalation

To use migrations, you'll need to install the EF Core CLI tool or package. This should be installed in the Api layer of your project.

+++ dotnet CLI
```
dotnet tool install --global dotnet-ef
```
+++ Package Manager Console
```
Install-Package Microsoft.EntityFrameworkCore.Tools
```
+++

Now you're ready to use Migrations.

## Usage

Before creating a migration, ensure that your `DbContext`, `Entity`, `Configurations/Database Mapping`, and `appsettings.json` are properly configured to avoid any errors.

## Creating a Migration

To create a migration, use: 

+++ dotnet CLI
```
dotnet ef migrations add <migration's name> -p "../<your_infra_project>"
```
+++ Package Manager Console
```
Add-Migration <migration's name> -P "../<your_infra_project>"
```
+++

Replace `<your_infra_project>` with the path to your infra project. For example:

`dotnet ef migrations add <migration's name> -p "../MyApi.Infra`

If executes successfully, a `Migrations` folder will be created in your Infra project containing the new migration.

## Migration Methods

### Up

The `Up` method defines the operations to apply the changes to the database schema. It includes all the fields that you specified in your configuration/mapping.

### Down 

The `Down` method defines the operations to revert the changes applied by the `Up` method. This method removes the updates from the database, rolling back the changes.

## Applying Migrations

To apply the migration, use: 

+++ dotnet CLI
```
dotnet ef database update
```
+++ Package Manager Console
```
Update-Database
```
+++

If executes successfully, you will have a new database with the updated schema.