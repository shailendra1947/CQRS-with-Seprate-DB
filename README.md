# CQRS with Separate Database

A modern implementation of the **Command Query Responsibility Segregation (CQRS)** pattern using **.NET Core**, featuring separate databases for read and write operations.

## 📋 Overview

This project demonstrates a clean architecture approach using CQRS principles to separate read and write operations into different models and data stores. This pattern enables better scalability, performance optimization, and independent scaling of read and write workloads.

### Key Features

- **CQRS Pattern Implementation** - Separate commands (write) and queries (read) operations
- **Separate Database Architecture** - Dedicated databases for read and write operations
- **Clean Architecture** - Well-organized layered structure
- **.NET Core** - Built with modern .NET Core framework
- **Scalable Design** - Independently scale read and write operations
- **Maintainable Code** - Clear separation of concerns

## 🏗️ Project Structure

```
CQRS-with-Seprate-DB/
├── Proyect.Domain/              # Domain layer - Business logic and entities
├── Proyect.Application/         # Application layer - Commands and queries handlers
├── Project.Infrastructure/      # Infrastructure layer - Data access and external services
├── Project.Tests/              # Unit and integration tests
├── WebAppCQRS/                 # Web application - API endpoints
└── ProyectCQRSnetCore.sln      # Solution file
```

### Layer Descriptions

- **Domain Layer** (`Proyect.Domain/`): Contains core business entities, value objects, and domain logic
- **Application Layer** (`Proyect.Application/`): Implements CQRS commands and query handlers, business workflows
- **Infrastructure Layer** (`Project.Infrastructure/`): Data access, database context, repository implementations
- **Presentation Layer** (`WebAppCQRS/`): ASP.NET Core Web API endpoints, controllers
- **Tests** (`Project.Tests/`): Unit and integration tests for the application

## 🚀 Getting Started

### Prerequisites

- .NET Core SDK (Version 6.0 or higher)
- SQL Server or compatible database
- Visual Studio 2022 or Visual Studio Code

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/shailendra1947/CQRS-with-Seprate-DB.git
   cd CQRS-with-Seprate-DB
   ```

2. **Restore dependencies**
   ```bash
   dotnet restore
   ```

3. **Configure database connections**
   - Update connection strings in `appsettings.json` for both write and read databases
   - Configure separate database contexts for command (write) and query (read) operations

4. **Run migrations**
   ```bash
   dotnet ef database update -p Project.Infrastructure
   ```

5. **Build the solution**
   ```bash
   dotnet build
   ```

6. **Run the application**
   ```bash
   dotnet run --project WebAppCQRS
   ```

## 📚 CQRS Pattern Explanation

### Commands (Write Operations)
Commands represent actions that modify state. Each command is handled by a specific handler that:
- Validates input
- Performs business logic
- Persists changes to the write database

### Queries (Read Operations)
Queries retrieve data without modifying state. Each query is handled by a specific handler that:
- Retrieves data from the read database
- Applies filtering and sorting
- Returns optimized data models for consumption

### Benefits

✅ **Scalability** - Scale read and write operations independently  
✅ **Performance** - Optimize each database for its specific workload  
✅ **Maintainability** - Clear separation of concerns  
✅ **Flexibility** - Use different technologies for read and write databases  
✅ **Testability** - Easier to test commands and queries in isolation  

## 🔧 Technology Stack

- **Framework**: .NET Core
- **Language**: C#
- **Architecture Pattern**: CQRS (Command Query Responsibility Segregation)
- **Database**: SQL Server (configurable)
- **API**: ASP.NET Core REST API

## 📖 Usage Examples

### Creating a Command Handler

```csharp
public class CreateProductCommand : IRequest<CreateProductResponse>
{
    public string Name { get; set; }
    public decimal Price { get; set; }
}

public class CreateProductCommandHandler : IRequestHandler<CreateProductCommand, CreateProductResponse>
{
    public async Task<CreateProductResponse> Handle(CreateProductCommand request, CancellationToken cancellationToken)
    {
        // Validate and process command
        // Save to write database
        // Return response
    }
}
```

### Creating a Query Handler

```csharp
public class GetProductByIdQuery : IRequest<ProductDto>
{
    public int ProductId { get; set; }
}

public class GetProductByIdQueryHandler : IRequestHandler<GetProductByIdQuery, ProductDto>
{
    public async Task<ProductDto> Handle(GetProductByIdQuery request, CancellationToken cancellationToken)
    {
        // Query read database
        // Return optimized data model
    }
}
```

## 🧪 Testing

Run tests using:

```bash
dotnet test
```

## 📝 Configuration

Configure application settings in `appsettings.json`:

```json
{
  "ConnectionStrings": {
    "WriteDb": "Server=.;Database=CQRS_Write;Trusted_Connection=true;",
    "ReadDb": "Server=.;Database=CQRS_Read;Trusted_Connection=true;"
  }
}
```



---

**Happy coding! 🎉**
