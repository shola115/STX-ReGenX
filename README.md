
# STX-ReGenX - Decentralized Renewable Energy Asset Management Protocol 

This Clarity smart contract enables decentralized registration, ownership, revenue-sharing, and governance of renewable energy assets (solar, wind, hydro, biomass) on the Stacks blockchain.

---

## 📚 Overview

The protocol allows stakeholders to:

* Register new energy assets
* Purchase tokenized shares of assets
* Receive STX revenue distributions
* Vote on governance proposals related to the assets

Each asset tracks ownership, performance metrics, and supports on-chain governance via a weighted voting mechanism.

---

## 🔐 Contract Constants

| Constant             | Value       | Description                                    |
| -------------------- | ----------- | ---------------------------------------------- |
| `CONTRACT-OWNER`     | `tx-sender` | Set at deployment; can distribute revenue      |
| `MIN-INVESTMENT`     | `u1000000`  | Minimum total capital for an asset (1 STX)     |
| `SHARE-SCALE`        | `u1000000`  | Used for calculating share-based voting power  |
| `VOTE-THRESHOLD`     | `u75`       | Proposal approval threshold (% of votes for)   |
| `MAINTENANCE-WINDOW` | `u144`      | Block window for time-based operations (\~24h) |

---

## ❗ Error Codes

| Code                      | Meaning                           |
| ------------------------- | --------------------------------- |
| `ERR-NOT-AUTHORIZED`      | Unauthorized sender               |
| `ERR-ASSET-EXISTS`        | Asset already exists              |
| `ERR-INVALID-AMOUNT`      | Provided value is invalid or zero |
| `ERR-ASSET-NOT-FOUND`     | Asset not found                   |
| `ERR-INSUFFICIENT-SHARES` | Not enough shares available       |
| `ERR-TRANSFER-FAILED`     | STX transfer failed               |
| `ERR-INVALID-NAME`        | Asset name is invalid             |
| `ERR-INVALID-ASSET-TYPE`  | Unsupported asset type            |
| `ERR-SELF-TRANSFER`       | Cannot transfer to self           |
| `ERR-ZERO-SHARES`         | Share amount is zero              |
| `ERR-PROPOSAL-ACTIVE`     | Proposal already active           |
| `ERR-PROPOSAL-EXPIRED`    | Proposal voting has ended         |
| `ERR-ALREADY-VOTED`       | Voter already voted               |
| `ERR-INVALID-STATUS`      | Asset status is not compatible    |
| `ERR-INSUFFICIENT-QUORUM` | Voting quorum was not met         |

---

## 🧱 Data Structures

### 1. `assets` (Map)

Stores registered energy assets with metadata including:

* Name, type (`solar`, `wind`, `hydro`, `biomass`)
* Total/available shares, share price
* Revenue metrics
* GPS location and timestamps

---

### 2. `ownership` (Map)

Tracks share ownership per user per asset with:

* Number of shares
* Voting power
* Claimed revenue
* Last claim height

---

### 3. `asset-metrics` (Map)

Tracks performance KPIs:

* Energy produced
* Operational hours
* Carbon offset
* ROI, efficiency, etc.

---

### 4. `governance-settings` (Map)

Configures governance parameters per asset:

* Quorum requirement
* Vote period
* Approval threshold
* Cooldown after voting ends

---

### 5. `proposals` (Map)

Each proposal contains:

* Proposer info, type, description
* Amount (for financial proposals)
* Vote counts and timing details
* Status and quorum flag

---

## ✅ Public Functions

### `register-asset(...)`

Register a new asset with name, type, share count, price, and GPS location.

### `purchase-shares(...)`

Buy a number of shares in an active asset using STX.

### `distribute-revenue(...)`

Distribute STX revenue across all shareholders.

### `submit-proposal(...)`

Submit a governance proposal if holding ≥5% of voting power.

---

## 🔍 Read-Only Functions

| Function                       | Purpose                          |
| ------------------------------ | -------------------------------- |
| `get-asset-info(asset-id)`     | Fetch metadata of an asset       |
| `get-ownership-info(...)`      | Get ownership details for a user |
| `get-asset-metrics(asset-id)`  | Get performance stats            |
| `get-governance-settings(...)` | View quorum and voting config    |
| `get-proposal-info(...)`       | View proposal details            |

---

## 🔐 Traits

Implements an `asset-owner-trait` with two stub functions:

* `transfer-ownership(...)`
* `claim-revenue(...)`

(These should be implemented in future extensions.)

---

## 🧪 Helper Functions

### Private Validations

* Name length & format
* Asset type validation
* Self-transfer prevention
* Voting power calculation

---

## 🚀 Deployment Notes

* Must deploy with `tx-sender` as the designated `CONTRACT-OWNER`
* Assets start with `status: "proposed"` and must be transitioned to `"active"` before purchase is allowed.

---

##  Future Improvements

* Implement `claim-revenue` and `transfer-ownership`
* Add proposal voting and execution functions
* Introduce asset activation workflow
* Add historical tracking or audit logs

---

## ✅ Example Use Case

1. Admin registers a solar farm asset.
2. Users buy shares once asset is "active".
3. STX revenue is distributed to shareholders.
4. A user submits a proposal to increase dividends.
5. Shareholders vote based on their voting power.

---

