<!-- PAGE_ID: broker-service_05_configuration-deployment -->
<details>
<summary>📚 Relevant source files</summary>

The following files were used as context for generating this wiki page:

- [Constants.cs:1-25](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/Helpers/Constants.cs#L1-L25)
- [appsettings.json:1-15](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/appsettings.json#L1-L15)
- [Dockerfile:1-29](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/Dockerfile#L1-L29)
- [BrokerService.test.csproj:1-25](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/test/BrokerService.test.csproj#L1-L25)
- [ci_workflow_1_gdzn.yml:1-13](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/.github/workflows/ci_workflow_1_gdzn.yml#L1-L13)
- [ci_workflow_2_1hth.yml:1-13](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/.github/workflows/ci_workflow_2_1hth.yml#L1-L13)

</details>

# Configuration, Build and Deployment

> **Related Pages**: [[Overview and Architecture|01_overview.md]]

---

<!-- BEGIN:AUTOGEN broker-service_05_configuration-deployment_config -->
## Configuration

Settings are read from configuration keys named in `Constants` ([Constants.cs:5-24](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/Helpers/Constants.cs#L5-L24)).

| Key | Purpose | Default in code |
|-----|---------|-----------------|
| `MSSQL_CONNECTIONSTRING` | SQL Server connection ([Constants.cs:9](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/Helpers/Constants.cs#L9)) | none |
| `PRICINGSERVICE_HOSTANDPORT` | Price service ([Constants.cs:5](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/Helpers/Constants.cs#L5)) | none |
| `ACCOUNTSERVICE_HOSTANDPORT` | Account service ([Constants.cs:6](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/Helpers/Constants.cs#L6)) | none |
| `ENGINE_HOSTANDPORT` | Engine notification target ([Constants.cs:7](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/Helpers/Constants.cs#L7)) | none |
| `PROXY_PREFIX` | Swagger server prefix ([Constants.cs:8](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/Helpers/Constants.cs#L8)) | empty ([Program.cs:58](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/Program.cs#L58)) |
| `FEATURE_FLAG_SERVICE_PROTOCOL`, `_BASE_URL`, `_PORT` | Feature flag service address ([Constants.cs:10-12](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/Helpers/Constants.cs#L10-L12)) | none |
| `FEATURE_FLAG_CACHE_DURATION_S` | Flag cache TTL ([Constants.cs:15](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/Helpers/Constants.cs#L15)) | 60 ([PluginManager.cs:12-17](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/ProblemPatterns/OpenFeature/PluginManager.cs#L12-L17)) |
| `HIGH_CPU_USAGE_REQUEST_DELAY_MS` | CPU burn duration ([Constants.cs:13](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/Helpers/Constants.cs#L13)) | 700 ([HighCpuUsageMiddleware.cs:14-19](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/ProblemPatterns/HighCpuUsage/HighCpuUsageMiddleware.cs#L14-L19)) |
| `HIGH_CPU_USAGE_CONCURRENCY` | CPU burn tasks ([Constants.cs:14](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/Helpers/Constants.cs#L14)) | 4 ([HighCpuUsageMiddleware.cs:21-26](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/ProblemPatterns/HighCpuUsage/HighCpuUsageMiddleware.cs#L21-L26)) |
| `MAINFRAME_SERVICE_URL` | Card validation backend ([Constants.cs:21](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/Helpers/Constants.cs#L21)) | none, fails open |
| `BuildVersion`, `BuildDate`, `BuildCommit` | Version endpoint ([Constants.cs:22-24](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/Helpers/Constants.cs#L22-L24)) | `{{BUILD_*}}` placeholders in appsettings ([appsettings.json:12-14](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/appsettings.json#L12-L14)) |

Log levels default to Information for the service and Warning for ASP.NET Core, EF Core and HttpClient ([appsettings.json:2-9](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/appsettings.json#L2-L9)).

Sources: [Constants.cs:1-25](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/Helpers/Constants.cs#L1-L25), [appsettings.json:1-15](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/appsettings.json#L1-L15)
<!-- END:AUTOGEN broker-service_05_configuration-deployment_config -->

---

<!-- BEGIN:AUTOGEN broker-service_05_configuration-deployment_build -->
## Docker Build, Tests and CI

The Dockerfile is a two-stage build. The SDK stage (`dotnet/sdk:8.0.412-alpine3.22`) copies `BrokerService/`, runs `dotnet test` on the test project and then `dotnet publish` ([Dockerfile:2-8](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/Dockerfile#L2-L8)). A failing test therefore fails the image build. The runtime stage (`dotnet/aspnet:8.0.18-alpine3.22`) installs `icu-libs`, creates a non-root `easytrade` user (uid/gid 3369) and runs `dotnet BrokerService.dll` ([Dockerfile:11-29](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/Dockerfile#L11-L29)). The image sets `ASPNETCORE_ENVIRONMENT=Development`, which enables Swagger ([Dockerfile:26](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/Dockerfile#L26), [Program.cs:53](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/Program.cs#L53)).

Tests use xUnit 2.9.3 and Moq 4.20.72 on `net8.0` ([BrokerService.test.csproj:3](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/test/BrokerService.test.csproj#L3), [BrokerService.test.csproj:11-12](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/test/BrokerService.test.csproj#L11-L12)). The test directory has unit tests (`TradeTests`, `LongTradeTests`, `BalanceTests`, `InstrumentTests`, `OpenFeatureTests`) and in-memory fakes for repositories and connectors under `test/Fakes`.

Two GitHub Actions workflows run on push and pull request. Each only echoes a greeting and sleeps 10 seconds to "simulate tests". They do not build or test the code ([ci_workflow_1_gdzn.yml:3-13](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/.github/workflows/ci_workflow_1_gdzn.yml#L3-L13), [ci_workflow_2_1hth.yml:3-13](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/.github/workflows/ci_workflow_2_1hth.yml#L3-L13)).

Sources: [Dockerfile:1-29](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/Dockerfile#L1-L29), [BrokerService.test.csproj:1-25](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/test/BrokerService.test.csproj#L1-L25), [ci_workflow_1_gdzn.yml:1-13](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/.github/workflows/ci_workflow_1_gdzn.yml#L1-L13)
<!-- END:AUTOGEN broker-service_05_configuration-deployment_build -->

---
