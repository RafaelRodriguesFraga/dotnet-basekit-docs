---
title: Welcome to DotnetBaseKit
sidebar_position: 1
order: 1
icon: "home"
label: Welcome
---

## Introduction

A comprehensive package designed to streamline the development process by providing pre-built components and architecture layers. DotnetBaseKit aims to simplify your workflow and enhance your productivity.

## What is DotnetBaseKit?

DotnetBaseKit is a collection of  components organized into different layers, each serving a specific purpose in the software development. By using these components, developers can focus on building core features and business logic without the need to reinvent the wheel for common functionalities.

## Components Overview
 *All of the components are using dotnet 6.0*
 
 - **DotnetBaseKit.Components.Api:** Provides API-related functionalities and abstractions for building RESTful services such as customized HTTP Responses.

 - **DotnetBaseKit.Components.Application:**  It is intended to be inherited by other service application classes to promote code reusability and maintain a consistent approach to handling notifications and related functionalities. It has Pagination classes as well.

 - **DotnetBaseKit.Components.Domain.Sql:** Defines domain entities, value objects, and domain logic for SQL Databases (MySQL, SQL Server and Postgres in this version) promoting a clean approach.

 - **DotnetBaseKit.Components.Domain.MongoDb:** Defines domain logic for MongoDB promoting a clean approach.

 - **DotnetBaseKit.Components.Infra.Sql:** Provides infrastructure components for SQL databases interactions, such as repositories and database context management.

 - **DotnetBaseKit.Components.Infra.MongoDb:** Offers infrastructure components for interacting with MongoDB databases, including repositories and data access abstractions.

 - **DotnetBaseKit.Components.Shared:** Contains shared utilities, extensions, and helper classes used across different layers of the application.

## Inspiration

This package was based on [Optsol.Components.Service](https://www.nuget.org/packages/Optsol.Components.Service). The whole set of components ( `DotnetBaseKit.Components.Api`, `DotnetBaseKit.Components.Application`, `DotnetBaseKit.Components.Domain.MongoDb`,  `DotnetBaseKit.Components.Domain.Sql`, `DotnetBaseKit.Components.Infra.MongoDb`, `DotnetBaseKit.Components.Infra.Sql`, `DotnetBaseKit.Components.Shared` ) is a basekit that was developed to make things a little bit easier for some people (and for learning purposes too) 

Ready to dive into DotnetBaseKit? Check out our comprehensive documentation to learn how to integrate and utilize each component effectively in your .NET projects. Whether you're a seasoned developer or just getting started, we've got you covered with detailed guides, tutorials, and examples.