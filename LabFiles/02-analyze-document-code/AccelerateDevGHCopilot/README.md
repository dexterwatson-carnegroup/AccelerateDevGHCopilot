# Library App

## Description

Library App is a .NET console application for managing a small library's patron and loan workflows. The application lets a user search for patrons, inspect patron details, review loaned books, return books, and extend active loans. Data is stored in JSON files and loaded through a simple repository layer, which makes the project easy to run locally without a database.

The solution is organized into separate projects for domain logic, console interaction, infrastructure, and tests. Dependency injection is configured at startup so the console application can work with services and repositories through interfaces.

## Project Structure

- src
  - Library.ApplicationCore
    - Entities
    - Enums
    - Interfaces
    - Services
    - Library.ApplicationCore.csproj
  - Library.Console
    - Json
    - appSettings.json
    - CommonActions.cs
    - ConsoleApp.cs
    - ConsoleState.cs
    - Program.cs
    - Library.Console.csproj
  - Library.Infrastructure
    - Data
    - Library.Infrastructure.csproj
- tests
  - UnitTests
    - ApplicationCore
    - LoanFactory.cs
    - PatronFactory.cs
    - UnitTests.csproj

## Key Classes and Interfaces

- `Program`
  - The application entry point. Builds configuration, registers dependencies, and starts the console workflow.
- `ConsoleApp`
  - Implements the interactive console experience, including patron search, patron details, and loan details screens.
- `IPatronRepository`
  - Defines patron data access operations such as searching for patrons, retrieving a patron by ID, and saving patron updates.
- `ILoanRepository`
  - Defines loan data access operations such as retrieving a loan by ID and saving loan updates.
- `IPatronService`
  - Defines business logic for renewing patron memberships.
- `ILoanService`
  - Defines business logic for returning books and extending loans.
- `PatronService`
  - Applies membership renewal rules, such as preventing early renewal or renewal when overdue loans exist.
- `LoanService`
  - Applies loan rules, such as blocking extensions for returned, expired, or membership-ineligible loans.
- `JsonData`
  - Loads and saves JSON data files, and populates related entities such as patrons, loans, books, and authors.
- `JsonPatronRepository`
  - Implements patron repository behavior using the shared JSON data source.
- `JsonLoanRepository`
  - Implements loan repository behavior using the shared JSON data source.

## Usage

### Prerequisites

- .NET 9 SDK or runtime
- A terminal or Visual Studio Code

### Run the application

From the `src/Library.Console` folder, run:

```bash
dotnet run