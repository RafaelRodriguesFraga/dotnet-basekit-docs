---
title: Api Layer
label: Api
order: 1;
---

## Overview

The `DotnetBaseKit.Components.Api` package provides common functionality for WebApi Applications. It has `ApiControllerBase` that extends the `ControllerBase` class from Microsoft.AspNetCore.Mvc and encapsulates common response creation and handling logic. 

## Installation

Install this package via dotnet CLI or Package Manager Console:

+++ dotnet CLI
```
dotnet add package DotnetBaseKit.Components.Api
```
+++ Package Manager Console
```
Install-Package DotnetBaseKit.Components.Api
```
+++

Now, you have to add add the dependency that contains Responses and Notifications. Feel free
to choose either the `Program.cs` approach or `Startup.cs` approach.

+++ Program.cs
```csharp #
builder.Services.AddApi();
```
+++ Startup.cs
```csharp #
// Put this inside your ConfigureServices method
services.AddApi();
```
+++

## Usage

With the dependencies added, you're ready to use it like below:

 ```csharp # 
using DotnetBaseKit.Components.Api.Base;
using DotnetBaseKit.Components.Api.Responses;
using Microsoft.AspNetCore.Mvc;
using TestApi.Application.Services;
using TestApi.Application.ViewModels;

namespace TestApi.Api.Controllers
{
    [Route("api/[controller]")]
    public class TestApiController : ApiControllerBase
    {
        private readonly ITestApiServiceApplication _testApiServiceApplication;

        public TestApiController(
            IResponseFactory responseFactory, 
            ITestApiServiceApplication testApiServiceApplication) 
            : base(responseFactory)
        {
            _testApiServiceApplication = testApiServiceApplication;
        }

        [HttpPost]
        public async Task<IActionResult> InsertAsync(TestApiViewModel viewModel)
        {
            await _testApiServiceApplication.CreateAsync(viewModel);

            return ResponseCreated();
        }
    }
}       
```

In this example, a TestService is called from the Application Layer. It accepts a `TestApiViewModel` object as a parameter, which represents the data to be inserted. It asynchronously calls the `CreateAsync` method of the `ITestApiServiceApplication` to perform the insertion. Upon successful, it returns a `Created` response using the `ResponseCreated` method previously mentioned.

