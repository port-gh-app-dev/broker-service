# Wiki Documentation Summary

Generated: 2026-10-30 16:41:28
Repository: BrokerService
Commit: `0e7f657163c06ac393c664199a474abcd896422c`

## Generation Status

**Overall Status**: ✅ Complete

| Metric | Expected | Actual | Status |
|--------|----------|--------|--------|
| Pages | 6 | 6 | ✅ |
| Sections | 14 | 14 | ✅ |
| Citations | - | 183 | ✅ |
| Diagrams | 4 | 4 valid | ✅ |

## Page Details

| Page | Title | Sections | Citations | Diagrams | Status |
|------|-------|----------|-----------|----------|--------|
| 01_overview.md | Overview and Architecture | 3/3 | 27 | 1 | ✅ |
| 02_api-reference.md | REST API Reference | 2/2 | 30 | 0 | ✅ |
| 03_trading-balances.md | Trading and Balance Logic | 3/3 | 33 | 2 | ✅ |
| 04_data-integrations.md | Data Model and External Services | 2/2 | 23 | 0 | ✅ |
| 05_configuration-deployment.md | Configuration, Build and Deployment | 2/2 | 37 | 0 | ✅ |
| 06_problem-patterns.md | Problem Patterns and Feature Flags | 2/2 | 33 | 1 | ✅ |

## Source Coverage

### Covered Files

- `.github/workflows/ci_workflow_1_gdzn.yml` - cited in 05_configuration-deployment.md
- `.github/workflows/ci_workflow_2_1hth.yml` - cited in 05_configuration-deployment.md
- `BrokerService/src/BrokerDbContext.cs` - cited in 01_overview.md, 04_data-integrations.md
- `BrokerService/src/BrokerService.csproj` - cited in 01_overview.md
- `BrokerService/src/Entities/Accounts/ServiceConnector/AccountServiceConnector.cs` - cited in 04_data-integrations.md
- `BrokerService/src/Entities/Balances/Balance.cs` - cited in 03_trading-balances.md, 04_data-integrations.md
- `BrokerService/src/Entities/Balances/Controllers/BalanceController.cs` - cited in 02_api-reference.md
- `BrokerService/src/Entities/Balances/Service/BalanceService.cs` - cited in 03_trading-balances.md
- `BrokerService/src/Entities/Instruments/Controllers/InstrumentController.cs` - cited in 02_api-reference.md
- `BrokerService/src/Entities/Instruments/OwnedInstrument.cs` - cited in 04_data-integrations.md
- `BrokerService/src/Entities/Prices/ServiceConnector/PriceServiceConnector.cs` - cited in 04_data-integrations.md
- `BrokerService/src/Entities/Trades/Controllers/TradeController.cs` - cited in 02_api-reference.md
- `BrokerService/src/Entities/Trades/Notification/TradeNotificationService.cs` - cited in 04_data-integrations.md
- `BrokerService/src/Entities/Trades/Service/LongTradeService.cs` - cited in 03_trading-balances.md
- `BrokerService/src/Entities/Trades/Service/TradeService.cs` - cited in 03_trading-balances.md, 04_data-integrations.md
- `BrokerService/src/Entities/Trades/Service/TradeServiceBase.cs` - cited in 03_trading-balances.md
- `BrokerService/src/Entities/Trades/Trade.cs` - cited in 03_trading-balances.md, 04_data-integrations.md
- `BrokerService/src/ExceptionHandling/BrokerExceptionFilter.cs` - cited in 02_api-reference.md
- `BrokerService/src/Helpers/ActionType.cs` - cited in 03_trading-balances.md
- `BrokerService/src/Helpers/BrokerServiceDependencyExtension.cs` - cited in 01_overview.md
- `BrokerService/src/Helpers/Constants.cs` - cited in 03_trading-balances.md, 04_data-integrations.md, 05_configuration-deployment.md, 06_problem-patterns.md
- `BrokerService/src/Helpers/TransactionalRepository.cs` - cited in 04_data-integrations.md
- `BrokerService/src/Program.cs` - cited in 01_overview.md, 05_configuration-deployment.md
- `BrokerService/src/Versioning/VersionController.cs` - cited in 02_api-reference.md
- `BrokerService/src/appsettings.json` - cited in 05_configuration-deployment.md
- `BrokerService/test/BrokerService.test.csproj` - cited in 05_configuration-deployment.md
- `Dockerfile` - cited in 05_configuration-deployment.md
- `README.md` - cited in 01_overview.md, 02_api-reference.md, 06_problem-patterns.md

## Issues

### Errors

None

### Recommendations

- None - documentation looks good!
