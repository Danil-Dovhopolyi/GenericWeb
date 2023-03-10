# GenericWebApi

This is a generic web project template. Users can clone it or create new repositories and extend it with domain logic for their purposes.

## About the project

- ASP.NET Core Web API project
- 3-layer architecture
- Entity Framework Core code first
- JWT Bearer auth
- FluentValidation, AutoMapper, AutoFilterer
- XUnit, Moq, FluentAssertions

## Current features

- Role-based auth using basic 'Admin', 'Moder' and 'User' roles
- Account confirmation through email
- Google authentication
- Admin controller for user CRUD
- Unit testing coverage
- CI process
- CD process

## Features planned

- Integration testing coverage

## Usage

Clone it to your PC and change the remote or click _Use this template_ -> _Create a new repository_

### Feature management

Some features are implemented with feature flags. To turn it on use `appsettings.json` section

```json
"FeatureManagement": {
    "EmailVerification": true,
    "GoogleAuthentication": true
  }
```

### Services

Services are added in `AddBusinessLogicServices` method with [Scrutor](https://github.com/khellang/Scrutor), so you don't need to add them explicitly. Services are added only from business layer assembly.

```C#
services.Scan(selector => selector
                .FromAssemblies(typeof(AssemblyReference).Assembly)
                .AddClasses(filter => filter.NotInNamespaceOf<ModelsNamespaceReference>(), publicOnly: false)
                .AsImplementedInterfaces()
                .WithScopedLifetime());
```

### Validation

Validation is implemented using `IModelValidator` interface. It finds appropriate validators using reflection and validates **business layer models**

```C#
public interface IModelValidator
{
    Result Validate<T>(T model) where T : class;
}
```

You can just add a validator to business layer assembly and it will be used by the `IModelValidator` implementation. <br>
Validation type is manual

```C#
var validationResult = _validator.Validate(model);
if (!validationResult.IsSuccess) return validationResult;
```

## CI/CD

These files can be viewed in github actions</br>
Unit test running and report publishing are present on PRs to dev</br>
Deployment to Azure as Web Service is present</br>

## Contributing

Pull requests are welcome

## Project status

I work on it when I have free time and I want
