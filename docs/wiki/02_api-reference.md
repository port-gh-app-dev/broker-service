<!-- PAGE_ID: broker-service_02_api-reference -->
<details>
<summary>📚 Relevant source files</summary>

The following files were used as context for generating this wiki page:

- [BalanceController.cs:1-57](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/Entities/Balances/Controllers/BalanceController.cs#L1-L57)
- [TradeController.cs:1-132](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/Entities/Trades/Controllers/TradeController.cs#L1-L132)
- [InstrumentController.cs:1-27](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/Entities/Instruments/Controllers/InstrumentController.cs#L1-L27)
- [VersionController.cs:1-31](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/Versioning/VersionController.cs#L1-L31)
- [BrokerExceptionFilter.cs:1-52](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/ExceptionHandling/BrokerExceptionFilter.cs#L1-L52)

</details>

# REST API Reference

> **Related Pages**: [[Trading and Balance Logic|03_trading-balances.md]]

---

<!-- BEGIN:AUTOGEN broker-service_02_api-reference_endpoints -->
## Endpoints

All controllers are `[ApiController]` classes. The balance, trade and instrument controllers apply `BrokerExceptionFilter` through `[TypeFilter]` ([BalanceController.cs:8-10](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/Entities/Balances/Controllers/BalanceController.cs#L8-L10), [TradeController.cs:8-10](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/Entities/Trades/Controllers/TradeController.cs#L8-L10), [InstrumentController.cs:8-10](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/Entities/Instruments/Controllers/InstrumentController.cs#L8-L10)).

| Method | Route | Purpose | Source |
|--------|-------|---------|--------|
| POST | `/v1/balance/{accountId}/deposit` | Deposit money, returns updated balance | ([BalanceController.cs:24-28](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/Entities/Balances/Controllers/BalanceController.cs#L24-L28)) |
| POST | `/v1/balance/{accountId}/withdraw` | Withdraw money, returns updated balance | ([BalanceController.cs:39-43](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/Entities/Balances/Controllers/BalanceController.cs#L39-L43)) |
| GET | `/v1/balance/{accountId}` | Current balance | ([BalanceController.cs:52-56](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/Entities/Balances/Controllers/BalanceController.cs#L52-L56)) |
| GET | `/v1/instrument?accountId=` | All instruments with price and owned amount; `accountId` defaults to 0 | ([InstrumentController.cs:21-26](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/Entities/Instruments/Controllers/InstrumentController.cs#L21-L26)) |
| POST | `/v1/trade/buy` | Quick buy | ([TradeController.cs:26-35](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/Entities/Trades/Controllers/TradeController.cs#L26-L35)) |
| POST | `/v1/trade/sell` | Quick sell | ([TradeController.cs:44-53](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/Entities/Trades/Controllers/TradeController.cs#L44-L53)) |
| POST | `/v1/trade/long/buy` | Register a long buy (amount, duration, price) | ([TradeController.cs:62-73](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/Entities/Trades/Controllers/TradeController.cs#L62-L73)) |
| POST | `/v1/trade/long/sell` | Register a long sell | ([TradeController.cs:82-93](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/Entities/Trades/Controllers/TradeController.cs#L82-L93)) |
| POST | `/v1/trade/long/process` | Process all long-running trades | ([TradeController.cs:98-103](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/Entities/Trades/Controllers/TradeController.cs#L98-L103)) |
| GET | `/v1/trade/{accountId}` | Paged trades; query `count`=10, `page`=0, `onlyOpen`, `onlyLong` | ([TradeController.cs:114-131](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/Entities/Trades/Controllers/TradeController.cs#L114-L131)) |
| GET | `/version` | Build info as plain text, or JSON when `Accept: application/json` | ([VersionController.cs:8-30](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/Versioning/VersionController.cs#L8-L30)) |

The version values come from the `BuildVersion`, `BuildDate` and `BuildCommit` settings and default to `"0"` ([VersionController.cs:12-17](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/Versioning/VersionController.cs#L12-L17)).

The README documents request bodies, such as `accountId`, `instrumentId` and `amount` for quick trades ([README.md:265-271](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/README.md#L265-L271)). Deposits also take `name`, `address`, `email`, `cardNumber`, `cardType` and `cvv` ([README.md:62-71](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/README.md#L62-L71)).

Sources: [BalanceController.cs:1-57](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/Entities/Balances/Controllers/BalanceController.cs#L1-L57), [TradeController.cs:1-132](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/Entities/Trades/Controllers/TradeController.cs#L1-L132), [InstrumentController.cs:1-27](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/Entities/Instruments/Controllers/InstrumentController.cs#L1-L27), [VersionController.cs:1-31](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/Versioning/VersionController.cs#L1-L31)
<!-- END:AUTOGEN broker-service_02_api-reference_endpoints -->

---

<!-- BEGIN:AUTOGEN broker-service_02_api-reference_errors -->
## Error Handling

`BrokerExceptionFilter` maps domain exceptions to HTTP status codes ([BrokerExceptionFilter.cs:16-28](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/ExceptionHandling/BrokerExceptionFilter.cs#L16-L28)):

| Exception | Status |
|-----------|--------|
| `AccountNotFoundException`, `InstrumentNotFoundException` | 404 |
| `NotEnoughMoneyException`, `NotEnoughAssetsException`, `NegativeAmountException` | 400 |
| `DbException` | 503 |
| anything else | 500 |

Handled errors return an `ErrorResponse` body and mark the exception handled ([BrokerExceptionFilter.cs:41-43](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/ExceptionHandling/BrokerExceptionFilter.cs#L41-L43)). For 500s the filter only logs, and the exception is not marked handled ([BrokerExceptionFilter.cs:35-39](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/ExceptionHandling/BrokerExceptionFilter.cs#L35-L39)).

Sources: [BrokerExceptionFilter.cs:11-51](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/ExceptionHandling/BrokerExceptionFilter.cs#L11-L51)
<!-- END:AUTOGEN broker-service_02_api-reference_errors -->

---
