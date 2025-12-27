🏗 Clean Architecture – Project Structure

This repository follows Clean Architecture, focusing on separation of concerns, framework independence, and high testability.

📁 Project Structure (High-Level)

🧱 Domain

⚡ Application

🔌 Infrastructure

🎭 Presentation (Web / API)

🔁 Dependency Rule

Dependencies always point inward

🔌 Infrastructure
    ↓
⚡ Application
    ↓
🧱 Domain

🎭 Presentation (Web / API)
    ↓
⚡ Application
    ↓
🧱 Domain

🧱 Domain Layer

The core of the system, containing pure business logic.
No dependency on frameworks, databases, or UI.

Responsibilities

Business rules and invariants

Entities & Value Objects

Domain Services & Domain Events

Constants, Enums, Domain Exceptions

Folder Structure

📂 Entities

Customer.cs – main domain entity containing business logic.

📂 ValueObjects

PhoneNumber.cs – immutable objects representing domain concepts.

🛠 DomainServices

CustomerDomainService.cs – business logic that doesn’t belong to a single entity.

🎉 DomainEvents

CustomerRegisteredEvent.cs – important events within the domain.

🔗 Interfaces

ICustomerRepository.cs – repository contracts (no implementation here).

🏷 Enums

CustomerStatus.cs – meaningful fixed values.

❌ Exceptions

DomainException.cs – domain-specific exceptions.

🔒 Constants

DomainConstants.cs – domain-wide constant values.

⚡ Application Layer

Implements use cases and coordinates domain entities.

Responsibilities

Use case execution / workflows

DTOs for input/output

Interfaces for repositories & external services

Validators & Mapping Profiles

Application-level services

Folder Structure

📂 UseCases → Customers/ImportCustomer/ImportCustomerUseCase.cs

🛠 Services → CustomerApplicationService.cs

📄 DTOs → ExternalCustomerDto.cs

🔗 Interfaces

Repositories → ICustomerRepository.cs

ApiClients → ICustomerApiClient.cs

✅ Validators → ImportCustomerValidator.cs

🖼 Mappings → CustomerMappingProfile.cs

🔄 Behaviors → LoggingBehavior.cs (for MediatR pipeline)

📦 Common → Result.cs

🔌 Infrastructure Layer

Technical implementations for Application layer interfaces.

Responsibilities

EF Core / database access

External API clients

Caching, messaging, file storage

Dependency Injection

Folder Structure

📂 Persistence

DbContext → AppDbContext.cs

Configurations → CustomerConfiguration.cs

Migrations

📂 Repositories → CustomerRepository.cs

🌐 ApiClients → CustomerApiClient.cs

📧 Messaging → EmailService.cs

🗄 Caching → RedisCacheService.cs

📁 Files → FileStorageService.cs

⚙ DependencyInjection → InfrastructureServiceCollection.cs

🎭 Presentation Layer (Web / API)

Entry point of the system, handles HTTP requests and user interaction.

Responsibilities

Controllers for endpoints

Request / Response models (Contracts)

Middleware & Filters

Composition Root (Program.cs / DI registration)

Folder Structure

📂 Controllers → CustomerController.cs

📄 Contracts

Requests → ImportCustomerRequest.cs

Responses → CustomerResponse.cs

⚙ Middlewares → ExceptionMiddleware.cs

🔒 Filters → AuthorizationFilter.cs

🧩 Extensions → PresentationServiceCollection.cs

Program.cs

appsettings.json

✅ Key Benefits of Clean Architecture

🧪 High testability & maintainability

💡 Clear separation of concerns

🔧 Framework-independent domain core

📈 Scalable for enterprise applications (Banking, ERP, Insurance)

🔄 Easy to extend & refactor
