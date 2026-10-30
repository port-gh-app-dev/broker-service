# Claude Instructions – BrokerService

This file provides guidance for Claude when working in this repository.

## Project overview

BrokerService is an ASP.NET Core 8 service that manages account balances and processes trades.  
See [README.md](./README.md) for full API documentation.

## Repository layout

```
BrokerService/
  src/   – application source (EasyTrade.BrokerService)
  test/  – xUnit unit tests   (EasyTrade.BrokerService.Test)
Dockerfile
README.md
```

## Prerequisites

- [.NET 8 SDK](https://dotnet.microsoft.com/download/dotnet/8.0) (matches `TargetFramework` in `.csproj` files)
- Docker (optional – only needed to build the container image)

## Install / restore dependencies

```bash
dotnet restore BrokerService/BrokerService.sln
```

## Build

```bash
dotnet build BrokerService/BrokerService.sln
```

## Run tests

```bash
dotnet test BrokerService/test/BrokerService.test.csproj
```

Run with verbose output:

```bash
dotnet test BrokerService/test/BrokerService.test.csproj --logger "console;verbosity=detailed"
```

## Lint / static analysis

The project uses the built-in .NET Roslyn analyser at `AnalysisLevel=latest-Minimum`.  
Warnings are surfaced during `dotnet build`. Treat new warnings as errors before committing:

```bash
dotnet build BrokerService/BrokerService.sln -warnaserror
```

## Docker build (optional)

```bash
docker build -t broker-service .
```

The Dockerfile runs `dotnet test` then `dotnet publish` as part of the image build, so a
failing test will also fail the Docker build.

## Key conventions

- **Nullable reference types** are enabled (`<Nullable>enable</Nullable>`). Always annotate new types correctly.
- **Implicit usings** are enabled; avoid redundant `using` directives.
- Follow the existing DI / repository / service layering pattern found under `BrokerService/src/Entities/`.
- Problem-pattern toggles are controlled via the feature-flag service (see `ProblemPatterns/` and the README).
- Environment variables referenced in code must be documented in the README.
