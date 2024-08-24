---
title: Application Layer
label: Application
order: 2;
---

## Overview

The `DotnetBaseKit.Components.Application` is part of the DotnetBaseKit architecture, designed to provide a foundational structure for various service applications. It is intended to be inherited by other service application classes to promote code reusability and maintain a consistent approach to handling notifications and related functionalities such as pagination.

# Installation

Install this package via dotnet CLI or Package Manager Console

+++ dotnet CLI
```
dotnet add package DotnetBaseKit.Components.Application
```
+++ Package Manager Console
```
Install-Package DotnetBaseKit.Components.Application
```
+++

Now, you have to add the dependency that contains Pagination and Notifications. Feel free
to choose either the `Program.cs` approach or `Startup.cs` approach.

+++ Program.cs
```csharp #
builder.Services.AddApplication();
```
+++ Startup.cs
```csharp #
// Put this inside your ConfigureServices method
services.AddApplication();
```
+++

## Usage

The primary purpose of the `BaseServiceApplication` class is to serve as a base class for other service application components. By inheriting from this class, developers can take advantage of its notification handling capabilities and maintain a consistent approach to managing notifications across the application.

With the dependencies added, you're ready to use it like below. You need to derive your service from `BaseServiceApplication`:

```csharp # 
using DotnetBaseKit.Components.Application.Base;
using DotnetBaseKit.Components.Shared.Notifications;

namespace YourNamespace
{
    public class YourServiceApplication : BaseServiceApplication, IYourServiceApplication
    {
        // interfaces
     
        public YourServiceApplication(NotificationContext notificationContext)
            : base(notificationContext)
        {
            // Initialize your interfaces
        }
            // implementation for IYourServiceApplication
    }
}  
``` 

In this package there's a `PaginationResponse` class. You can see how to use here:

[!ref Go to Pagination](/how-to-use/pagination)

In practice, developers can create new service applications by inheriting from the `BaseServiceApplication` class and implementing the necessary business logic specific to their use case. The constructor ensures that each service application instance has access to a shared `NotificationContext` instance for handling notifications.


