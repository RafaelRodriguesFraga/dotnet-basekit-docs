---
title: Pagination
label: Pagination
order: 2;
---

## Class Overview

The PaginationResponse class within the `DotnetBaseKit.Components.Application.Pagination` namespace is a component designed to handle pagination-related responses in the DotnetBaseKit application. It implements the `IPaginationResponse<TData>` interface and is designed to be a versatile response structure that contains pagination-related information along with a collection of data.

##  Usage

Developers can use this class when implementing methods that return paginated data. By utilizing the `PaginationResponse` class, developers can ensure consistent and predictable responses that include the data collection, current page number, total pages, and total record count.

The following method is used in `DotnetBaseKit` to retrieve paginated data. It returns a tuple with the result set and the total record count:

```csharp #   
    public async Task<(IEnumerable<TEntity> result, int totalRecords)> GetAllPaginatedAsync(int page, int quantityPerPage)
    {
        var skip = page == 1 ? 0 : (page - 1) * quantityPerPage;

        var totalRecords = Set.Count();

        var result = await Set
                 .Skip(skip)
                 .Take(quantityPerPage)
                 .OrderByDescending(p => p.CreatedAt)
                 .ToListAsync();

        return (result, totalRecords);
    }
  
``` 
You can use this method in your `ServiceApplication` classes. First, in your interface, create a method like this:

```csharp #
using DotnetBaseKit.Components.Application.Pagination;
// other usings 

namespace YourNamespace.Application.Services
{
    public interface IYourServiceApplication
    {
       // other methods
       
        Task<PaginationResponse<YourClass>> GetAllPaginatedAsync(int page, int quantityPerPage);        
    }
}
```

Then, implement the method like this:

```csharp #
using DotnetBaseKit.Components.Application.Base;
using DotnetBaseKit.Components.Application.Pagination;
using DotnetBaseKit.Components.Shared.Notifications;
using YourNamespace.Domain.Repositories;

namespace YourNamespace.Application.Services
{
    public class YourServiceApplication : BaseServiceApplication, IYourServiceApplication
    {
        private readonly IYourReadRepository _yourReadRepository;

        public YourServiceApplication(
            NotificationContext notificationContext, 
            IYourSqlReadRepository yourSqlReadRepository) : base(notificationContext)
        {
            _yourSqlWriteRepository = yourSqlWriteRepository;
            _yourSqlReadRepository = yourSqlReadRepository;
        }

        public async Task<PaginationResponse<YourClass>> GetAllPaginatedAsync(int currentPage, int quantityPerPage)
        {
            var (result, totalRecords) = await _yourReadRepository.FindAllPaginatedAsync(currentPage, quantityPerPage);

            return new PaginationResponse<YourClass>(currentPage, quantityPerPage, totalRecords, result);
        }  
    }
}
```

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

This Pagination is only available to relational databases in this version. MongoDB Pagination will be added in the future.


