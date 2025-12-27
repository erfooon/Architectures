🏗 Architectures

Clean Architecture – Project Layout
This repository follows Clean Architecture, focusing on separation of concerns, testability, and independence from frameworks and technologies.

📁 Solution Structure
src
│
├── Domain
├── Application
├── Infrastructure
└── Presentation (Web / API)

🧠 Dependency Rule (Core Principle)

Dependencies always point inward
Infrastructure
    ↓
Application
    ↓
Domain
----------------
Web (API / MVC)
    ↓
Application
    ↓
Domain

Inner layers never depend on outer layers
Business logic is isolated and framework-agnostic

1️⃣ Domain Layer (Core Business)

📌 Contains pure business rules and models

📌 No dependency on frameworks, databases, or UI

Domain
│
├── Entities
│   └── Customer.cs
│
├── ValueObjects
│   └── PhoneNumber.cs
│
├── DomainServices
│   └── CustomerDomainService.cs
│
├── DomainEvents
│   └── CustomerRegisteredEvent.cs
│
├── Interfaces
│   └── ICustomerRepository.cs
│
├── Enums
│   └── CustomerStatus.cs
│
├── Exceptions
│   └── DomainException.cs
│
└── Constants
    └── DomainConstants.cs

Responsibilities:
Business rules and invariants
Entities and Value Objects
Domain-specific logic
No technical or infrastructure concerns

2️⃣ Application Layer (Use Cases)
📌 Contains application-specific business logic
📌 Orchestrates Domain objects to fulfill system use cases

Application
│
├── UseCases
│   └── Customers
│       └── ImportCustomer
│           └── ImportCustomerUseCase.cs
│
├── Services
│   └── CustomerApplicationService.cs
│
├── DTOs
│   └── ExternalCustomerDto.cs
│
├── Interfaces
│   ├── Repositories
│   │   └── ICustomerRepository.cs
│   │
│   └── ApiClients
│       └── ICustomerApiClient.cs
│
├── Validators
│   └── ImportCustomerValidator.cs
│
├── Mappings
│   └── CustomerMappingProfile.cs
│
├── Behaviors
│   └── LoggingBehavior.cs   (MediatR Pipeline)
│
└── Common
    └── Result.cs

Responsibilities:
Use case execution
Input validation
DTO definitions
Interfaces (contracts) for persistence and external services
Application-level workflows

3️⃣ Infrastructure Layer (Technical Details)
📌 Contains implementations of interfaces
📌 Handles external concerns like databases, APIs, caching, messaging

Infrastructure
│
├── Persistence
│   ├── DbContext
│   │   └── AppDbContext.cs
│   │
│   ├── Configurations
│   │   └── CustomerConfiguration.cs
│   │
│   └── Migrations
│
├── Repositories
│   └── CustomerRepository.cs
│
├── ApiClients
│   └── CustomerApiClient.cs
│
├── Messaging
│   └── EmailService.cs
│
├── Caching
│   └── RedisCacheService.cs
│
├── Files
│   └── FileStorageService.cs
│
└── DependencyInjection
    └── InfrastructureServiceCollection.cs

Responsibilities:
EF Core & database access
External API communication
File system, caching, messaging
Dependency Injection configuration

4️⃣ Presentation Layer (Web / API)
📌 Entry point of the system
📌 Handles HTTP communication and user interaction

Presentation
│
├── Controllers
│   └── CustomerController.cs
│
├── Contracts
│   ├── Requests
│   │   └── ImportCustomerRequest.cs
│   │
│   └── Responses
│       └── CustomerResponse.cs
│
├── Middlewares
│   └── ExceptionMiddleware.cs
│
├── Filters
│   └── AuthorizationFilter.cs
│
├── Extensions
│   └── PresentationServiceCollection.cs
│
├── Program.cs
└── appsettings.json

Responsibilities:
HTTP endpoints
Request / Response models
Middleware and filters
Composition Root (DI registration)
No business logic

✅ Architecture Benefits

✔ High testability
✔ Clear separation of concerns
✔ Framework-independent core
✔ Scalable and maintainable
✔ Suitable for enterprise systems (Banking, ERP, Insurance)
