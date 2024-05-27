---
title: Responses
label: Responses
order: 1;
---

## Overview

These response methods are part of the DotnetBaseKit.Components.Api library. For detailed information on installation and usage, please refer to the [Api in Components Section](../Components/api).

DotnetBaseKit.Components.Api offers a suite of methods designed to enhance the readability and structure of your API responses, including `CreateResponse`, `ResponseCreated()`, `ResponseOk()`(and others variations), and `ResponseBadRequest()`. These methods simplify the process of generating consistent and meaningful HTTP responses across your application.

## Constructors

The `ApiControllerBase` class provides a single constructor that accepts an `IResponseFactory` parameter. This constructor is used to inject an instance of the response factory, which is responsible for creating API responses. Example usage:

```csharp #
using DotnetBaseKit.Components.Api.Base;
using DotnetBaseKit.Components.Api.Responses;
using Microsoft.AspNetCore.Mvc;

namespace YourNamespace.Api.Controllers
{
    [Route("api/[controller]")]
    public class TestApiController : ApiControllerBase
    {
        public YourController(IResponseFactory responseFactory)
        {

        }
    }
}
```

Inherit you Controller from `ApiControllerBase`.

## Methods

### `CreateResponse()`

This method creates a basic API response using the injected response factory. It returns an `IActionResult` representing the HTTP response. If the response's `Success` property is `false`, a BadRequest response is returned. Otherwise, an Ok response is returned with the response object.

Here’s an example of how to implement this in an Controller:

```csharp #
using DotnetBaseKit.Components.Api.Base;
using DotnetBaseKit.Components.Api.Responses;
using Microsoft.AspNetCore.Mvc;

namespace YourNamespace.Api.Controllers
{
    [Route("api/[controller]")]
    public class YourController : ApiControllerBase
    {
        public YourController(IResponseFactory responseFactory)
        {

        }

        [HttpGet]
        public async Task<IActionResult> GetAsync()
        {
            return CreateResponse();
        }
    }
}
```

If there are no errors, the response will look like this:

```json
{
  "success": true,
  "errors": []
}
```

If something goes wrong, the response will include the error details (these errors comes from the notifications):

```json
{
  "success": false,
  "errors": ["Error: Your error"]
}
```

### `ResponseOk<TData>(TData result)`

This method creates an API response with a single data object of type `TData`. It returns an `IActionResult` representing the HTTP response. If the response's `Success` property is `false`, a BadRequest response is returned. Otherwise, an Ok response is returned with the response object.

Here’s an example of how to implement this in an ASP.NET Core controller:

```csharp #
using DotnetBaseKit.Components.Api.Base;
using DotnetBaseKit.Components.Api.Responses;
using Microsoft.AspNetCore.Mvc;
using YourNamespace.Application.Services;

namespace YourNamespace.Api.Controllers
{
    [Route("api/[controller]")]
    public class YourController : ApiControllerBase
    {
        private readonly IYourServiceApplication _yourServiceApplication;

        public YourController(IResponseFactory responseFactory, IYourServiceApplication  yourServiceApplication)
        {
           _yourServiceApplication = yourServiceApplication;
        }

        // other methods...

        [HttpGet("{id}")]
        public async Task<IActionResult> GetByIdAsync(Guid id)
        {
            var result = await _yourServiceApplication.GetByIdAsync(id);

            return ResponseOk(result);
        }

    }
}
```

In this example, the `GetByIdAsync()` method is called from a service, and the result is passed to the ResponseOk method.

If there are no errors, the response will look like this:

```json #
{
  "data": {
    "someField": "Some data",
    "id": "84606833-6cb6-46d5-be56-c86e5dbd59cc",
    "createdAt": "2024-05-24T22:41:46.594367"
  },
  "success": true,
  "errors": []
}
```

If something goes wrong, the response will include the error details (this error comes from the notifications):

```json
{
  "success": false,
  "errors": ["Error: Your error"]
}
```

### `ResponseOk<TData>(IEnumerable<TData> result)`

This method creates an API response with a collection of data objects of type `TData`. It returns an `IActionResult` representing the HTTP response. If the response's `Success` property is `false`, a BadRequest response is returned. Otherwise, an Ok response is returned with the response object.

Here's an example of how to implement this in an Controller:

```csharp #
using DotnetBaseKit.Components.Api.Base;
using DotnetBaseKit.Components.Api.Responses;
using Microsoft.AspNetCore.Mvc;
using YourNamespace.Application.Services;

namespace YourNamespace.Api.Controllers
{
    [Route("api/[controller]")]
    public class YourController : ApiControllerBase
    {
        private readonly IYourServiceApplication _yourServiceApplication;

        public YourController(IResponseFactory responseFactory, IYourServiceApplication  yourServiceApplication)
        {
           _yourServiceApplication = yourServiceApplication;
        }

        // other methods...

        [HttpGet]
        public async Task<IActionResult> GetAllAsync()
        {
            var result = await _yourServiceApplication.GetAllAsync();

            return ResponseOk(result);
        }

    }
}
```

In this example, the `GetAllAsync` method is called from a service, and the result is passed to the ResponseOk method.

If there are no errors, the response will look like this:

```json #
{
  "data": [
    {
      "someField": "Some data",
      "id": "84606833-6cb6-46d5-be56-c86e5dbd59cc",
      "createdAt": "2024-05-24T22:41:46.594367"
    },
    {
      "someField": "Some data 2",
      "id": "dbb83e77-befc-4c84-b903-fab09f2eadfe",
      "createdAt": "2024-05-24T22:41:46.594367"
    }
  ],
  "success": true,
  "errors": []
}
```

If no data is present, the response will contain an empty array:

```json #
{
  "data": [],
  "success": true,
  "errors": []
}
```

### `ResponseOk<TData>(PaginationResponse<TData> searchResult)`

This method creates an API response with a pagination result of type `PaginationResponse<TData>`. It returns an `IActionResult` representing the HTTP response. If the response's `Success` property is `false`, a BadRequest response is returned. Otherwise, an Ok response is returned with the response object paginated.

Here’s an example of how to implement this in an Controller:

```csharp #
using DotnetBaseKit.Components.Api.Base;
using DotnetBaseKit.Components.Api.Responses;
using Microsoft.AspNetCore.Mvc;
using YourNamespace.Application.Services;

namespace YourNamespace.Api.Controllers
{
    [Route("api/[controller]")]
    public class YourController : ApiControllerBase
    {
        private readonly IYourServiceApplication _yourServiceApplication;

        public YourController(IResponseFactory responseFactory, IYourServiceApplication  yourServiceApplication)
        {
           _yourServiceApplication = yourServiceApplication;
        }

        // other methods...

        [HttpGet]
        public async Task<IActionResult> GetAllPaginatedAsync([FromQuery] int page, [FromQuery] int  quantityPerPage)
        {
            var result = await _yourServiceApplication.GetAllPaginatedAsync(page, quantityPerPage);

            return ResponseOk(result);
        }
    }
}
```

In this example, the `GetAllPaginatedAsync` method is called from a service, and the result is passed to the `ResponseOk` method.

If there are no errors, the response will look like this:

```json #
{
  "currentPage": 1,
  "quantityPerPage": 10,
  "totalRecords": 2,
  "totalPages": 1,
  "data": [
    {
      "someField": "Some data",
      "id": "84606833-6cb6-46d5-be56-c86e5dbd59cc",
      "createdAt": "2024-05-24T22:41:46.594367"
    },
    {
      "someField": "Some data 2",
      "id": "dbb83e77-befc-4c84-b903-fab09f2eadfe",
      "createdAt": "2024-05-24T22:41:46.594367"
    }
  ],
  "success": true,
  "errors": []
}
```

### `ResponseCreated<TData>(TData result)`

This method creates an API response for a successful resource creation operation. It returns an `IActionResult` representing the HTTP response. If the response's `Success` property is `false`, a BadRequest response is returned. Otherwise, a Created response (HTTP 201) is returned with the response object.

Here’s an example of how to implement this in an Controller:

```csharp # 
using DotnetBaseKit.Components.Api.Base;
using DotnetBaseKit.Components.Api.Responses;
using Microsoft.AspNetCore.Mvc;
using YourNamespace.Application.Services;
using YourNamespace.Application.ViewModels;

namespace YourNamespace.Api.Controllers
{
    [Route("api/[controller]")]
    public class YourController : ApiControllerBase
    {
         private readonly IYourServiceApplication _yourServiceApplication;
         public YourController(IResponseFactory responseFactory, IYourServiceApplication yourServiceApplication) 
             : base(responseFactory)
         {
             _yourServiceApplication = yourServiceApplication;
         }

         [HttpPost]
         public async Task<IActionResult> InsertAsync(YourViewModel viewModel)
         {
             await _yourServiceApplication.CreateAsync(viewModel);

             return ResponseCreated(viewModel);
         }
    }
}   
```

In this example, the `CreateAsync()` method is called from a service, and the result is passed to the `ResponseCreated` method.

If there are no errors, the response will look like this:

```json #
{
  "data": {
    "someField": "Some data",
    "id": "84606833-6cb6-46d5-be56-c86e5dbd59cc",
    "createdAt": "2024-05-24T22:41:46.594367"
  },
  "success": true,
  "errors": []
}
```

If something goes wrong, the response will include the error details (this error comes from the notifications):

```json
{
  "success": false,
  "errors": ["Error: Your error"]
}
```

### `ResponseCreated()`

This method creates a basic API response for a successful resource creation operation. It returns an `IActionResult` representing the HTTP response. If the response's `Success` property is `false`, a BadRequest response is returned. Otherwise, a Created response (HTTP 201) is returned with the response object.

Here’s an example of how to implement this in an Controller:

```csharp # 
using DotnetBaseKit.Components.Api.Base;
using DotnetBaseKit.Components.Api.Responses;
using Microsoft.AspNetCore.Mvc;
using YourNamespace.Application.Services;
using YourNamespace.Application.ViewModels;

namespace YourNamespace.Api.Controllers
{
    [Route("api/[controller]")]
    public class YourController : ApiControllerBase
    {
         private readonly IYourServiceApplication _yourServiceApplication;
         public YourController(IResponseFactory responseFactory, IYourServiceApplication yourServiceApplication) 
             : base(responseFactory)
         {
             _yourServiceApplication = yourServiceApplication;
         }

         [HttpPost]
         public async Task<IActionResult> InsertAsync(YourViewModel viewModel)
         {
             await _testApiServiceApplication.CreateAsync(viewModel);

             return ResponseCreated();
         }
    }
}   
```

In this example, the `CreateAsync()` method is called from a service like the other above. The difference is that you don't pass anything to the `ResponseCreated` method.

If there are no errors, the response will look like this:

```json
{
  "success": true,
  "errors": []
}
```

If something goes wrong, the response will include the error details (this error comes from the notifications):

```json
{
  "success": false,
  "errors": ["Error: Your error"]
}
```

### `ResponseBadRequest<TData>(TData result)`

This method creates a BadRequest response with the provided data object. It returns an `IActionResult` representing the HTTP Response BadRequest (400).

This is used to indicate that an error has occurred. The result can contain any JSON object of the specific error types mentioned above.