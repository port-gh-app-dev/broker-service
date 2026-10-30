<!-- PAGE_ID: broker-service_04_data-integrations -->
<details>
<summary>📚 Relevant source files</summary>

The following files were used as context for generating this wiki page:

- [BrokerDbContext.cs:1-38](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/BrokerDbContext.cs#L1-L38)
- [OwnedInstrument.cs:1-21](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/Entities/Instruments/OwnedInstrument.cs#L1-L21)
- [TransactionalRepository.cs:1-15](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/Helpers/TransactionalRepository.cs#L1-L15)
- [PriceServiceConnector.cs:1-71](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/Entities/Prices/ServiceConnector/PriceServiceConnector.cs#L1-L71)
- [AccountServiceConnector.cs:1-41](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/Entities/Accounts/ServiceConnector/AccountServiceConnector.cs#L1-L41)
- [TradeNotificationService.cs:1-43](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/Entities/Trades/Notification/TradeNotificationService.cs#L1-L43)

</details>

# Data Model and External Services

> **Related Pages**: [[Trading and Balance Logic|03_trading-balances.md]]

---

<!-- BEGIN:AUTOGEN broker-service_04_data-integrations_db -->
## Database Model

`BrokerDbContext` exposes `Balances`, `BalanceHistories`, `Instruments`, `OwnedInstruments`, `Packages`, `Products` and `Trades` ([BrokerDbContext.cs:14-20](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/BrokerDbContext.cs#L14-L20)). Every `decimal` property is configured with precision 18 and scale 8 ([BrokerDbContext.cs:22-37](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/BrokerDbContext.cs#L22-L37)).

Entity details seen in source:

- `Balance` is keyed by `AccountId` and mapped to table `Balance` ([Balance.cs:7-12](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/Entities/Balances/Balance.cs#L7-L12)).
- `OwnedInstrument` maps to table `Ownedinstruments` and holds account, instrument, quantity and last modification date ([OwnedInstrument.cs:5-17](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/Entities/Instruments/OwnedInstrument.cs#L5-L17)).
- `Trade` has direction, quantity, entry price, open/close timestamps, `TradeClosed`, `TransactionHappened` and `Status` ([Trade.cs:18-28](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/Entities/Trades/Trade.cs#L18-L28)).

Repositories inherit `TransactionalRepository`, which exposes begin, commit, rollback and save so services never touch the `DbContext` directly ([TransactionalRepository.cs:3-14](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/Helpers/TransactionalRepository.cs#L3-L14)).

Sources: [BrokerDbContext.cs:12-38](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/BrokerDbContext.cs#L12-L38), [TransactionalRepository.cs:1-15](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/Helpers/TransactionalRepository.cs#L1-L15)
<!-- END:AUTOGEN broker-service_04_data-integrations_db -->

---

<!-- BEGIN:AUTOGEN broker-service_04_data-integrations_connectors -->
## Service Connectors

| Connector | Target | Behavior |
|-----------|--------|----------|
| `PriceServiceConnector` | `http://{PRICINGSERVICE_HOSTANDPORT}/` | `GET v1/prices/instrument/{id}?records=n` and `GET v1/prices/latest`. A non-200 response is logged and returns an empty list ([PriceServiceConnector.cs:17-57](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/Entities/Prices/ServiceConnector/PriceServiceConnector.cs#L17-L57)) |
| `AccountServiceConnector` | `http://{ACCOUNTSERVICE_HOSTANDPORT}/api/` | `GET accounts/{id}`. A non-200 response throws `AccountNotFoundException` ([AccountServiceConnector.cs:17-33](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/Entities/Accounts/ServiceConnector/AccountServiceConnector.cs#L17-L33)) |
| `TradeNotificationService` | `http://{ENGINE_HOSTANDPORT}/api/trade/scheduler/notification` | Fire-and-forget POST of the closed trade. Failures are only logged ([TradeNotificationService.cs:15-42](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/Entities/Trades/Notification/TradeNotificationService.cs#L15-L42)) |

`GetLastPriceByInstrumentId` requests a single record and returns the first, or null ([PriceServiceConnector.cs:59-63](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/Entities/Prices/ServiceConnector/PriceServiceConnector.cs#L59-L63)). Quick trades dereference it with `!`, so an unavailable price service would surface as a null dereference ([TradeService.cs:80](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/Entities/Trades/Service/TradeService.cs#L80)).

The host-and-port constants are defined in `Constants` ([Constants.cs:5-7](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/Helpers/Constants.cs#L5-L7)).

Sources: [PriceServiceConnector.cs:1-71](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/Entities/Prices/ServiceConnector/PriceServiceConnector.cs#L1-L71), [AccountServiceConnector.cs:1-41](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/Entities/Accounts/ServiceConnector/AccountServiceConnector.cs#L1-L41), [TradeNotificationService.cs:1-43](https://github.com/port-gh-app-dev/broker-service/blob/0e7f657163c06ac393c664199a474abcd896422c/BrokerService/src/Entities/Trades/Notification/TradeNotificationService.cs#L1-L43)
<!-- END:AUTOGEN broker-service_04_data-integrations_connectors -->

---
