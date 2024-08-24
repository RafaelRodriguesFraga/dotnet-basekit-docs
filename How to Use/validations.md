---
title: Validations
label: Validations
order: 3;
---

Validation ensures that the data being processed by your application adheres to predefined rules, helping to maintain data integrity and prevent errors. Implementing validation can catch issues early in the workflow, providing immediate feedback to users and developers when data does not meet the required criteria.

To get started with validation, you need to install the `FluentValidation` package. This package provides a fluent interface for building strongly-typed validation rules. Remember to install it in your Domain Layer.

+++ dotnet CLI
```
dotnet add package FluentValidation
```
+++ Package Manager Console
```
Install-Package FluentValidation
```
+++

## Creating a Validator for Your DTO

Here's an example of how to create a validation class for a DTO using FluentValidation:

```csharp #
using YourNamespace.Domain.DTOs;
using YourNamespace.Domain.Entities;
using FluentValidation;

namespace YourNamepace.Domain.Validations
{
    public class YourDtoContract : AbstractValidator<YourDto>
    {
        public YourDtoContract()
        {
            RuleFor(x => x.Field1)
                .NotEmpty()
                .WithMessage("Field 1 name cannot be empty.");

            RuleFor(x => x.Field2)
              .GreaterThan(0)
              .WithMessage("Field 2 must be greater than 0.");       
        }
    }
}
```

For more information on `FluentValidation`, you can see the official documentation [here](https://docs.fluentvalidation.net/en/latest/)

## Using the Validation Class

You can use your validation class inside the `Validate()` method, along with the `AddNotification()` method:

```csharp #
using DotnetBaseKit.Components.Domain.Sql.Dtos.Base;

namespace YourNamespace.Dtos
{
    public class YourDto : BaseDto
    {
        public string Field1 { get; set; } = string.Empty;
        public decimal Field2 { get; set; }

        public override void Validate()
        {
            var validation = new YourDtoContract();
            var validationResult = validation.Validate(this);

            AddNotifications(validationResult);            
        }
    }
}
```

## Implementing Validation in Service Application Methods

Here's how you can use the validated DTO in your `ServiceApplication` methods:

```csharp #
using DotnetBaseKit.Components.Application.Base;
using DotnetBaseKit.Components.Application.Pagination;
using DotnetBaseKit.Components.Shared.Notifications;
using YourNamespace.Domain.Repositories;
using YourNamespace.Domain.DTOs;

namespace YourNamespace.Application.Services
{
    public class YourServiceApplication : BaseServiceApplication, IYourServiceApplication
    {
        private readonly IYourWriteRepository _yourWriteRepository;

        public YourServiceApplication(
            NotificationContext notificationContext, 
            IYourWriteRepository yourWriteRepository) : base(notificationContext)
        {
            _yourWriteRepository = yourWriteRepository;
        }

        public async Task CreateAsync(YourDto dto)
        {
            dto.Validate();
            var dtoHasErrors = dto.Invalid;
            if (dtoHasErrors)
            {
                _notificationContext.AddNotifications(dto.Notifications);
                return;
            }

            await _writeRepository.InsertAsync(dto);

        }
    }
}
```

When the `YourDto` data is validated and an error occurs, the `Validate()` method will flag the DTO as invalid. The validation errors defined in `YourDtoContract` will be added to the notification context.

In your API requests, if any of these errors occur, the response will look like this:

```json
{
  "success": false,
  "errors": [
    "Field1: Field 1 name cannot be empty",
    "Field2: Field 2 must be greater than 0."
  ]
}
```

This setup ensures that your application handles data validation consistently and provides clear feedback when validation rules are not met, enhancing the robustness and user experience of your application.

