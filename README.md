# EmeraldVault

EmeraldVault is a Paper plugin that turns emeralds into a virtual bank economy with GUI banking, bank levels, savings, scheduled interest, player payments, auto-deposit, bank-funded villager trades, transaction history, Vault support, and PlaceholderAPI placeholders.

## Requirements

- Paper 1.21.x
- Java 21
- Optional: Vault
- Optional: PlaceholderAPI
- Optional: Essentials or another plugin that uses Vault economy

The plugin jar is built as `EmeraldVault.jar`.

## Installation

1. Put `EmeraldVault.jar` into your server `plugins` folder.
2. Start the server once.
3. Edit `plugins/EmeraldVault/config.yml` and `plugins/EmeraldVault/messages.yml`.
4. Restart the server or run `/emv reload`.

Important: change `admin.resetall-password` before using `/emv resetall PASSWORD`.

## Player Commands

| Command | Description |
| --- | --- |
| `/bank` | Opens the main bank GUI. |
| `/bank help` | Shows player commands. |
| `/bank upgrade` | Upgrades your bank to the next level if you meet the requirements. |
| `/bank autodeposit` | Toggles auto-deposit if unlocked and enabled in config. |
| `/bank bankfund` | Toggles bank-funded villager trades if unlocked and enabled in config. |
| `/balance` | Shows your bank balance. If emeralds are in hand, it also shows hand and total. |
| `/bal` | Alias for `/balance`. |
| `/balance <player>` | Shows another player's bank balance. |
| `/bal <player>` | Alias for `/balance <player>`. |
| `/deposit` | Deposits all valid emeralds from your inventory into your bank. |
| `/deposit all` | Deposits all valid emeralds. |
| `/deposit half` | Deposits half of valid emeralds. |
| `/deposit <amount>` | Deposits a specific amount. |
| `/withdraw` | Withdraws the configured default amount, `64` by default, or the full balance if under that. |
| `/withdraw all` | Withdraws all available bank balance that can fit in the inventory. |
| `/withdraw half` | Withdraws half of the bank balance. |
| `/withdraw <amount>` | Withdraws a specific amount. |
| `/pay <player> <amount>` | Sends bank balance to another player. |
| `/interest` | Shows time until the next interest payout. |
| `/baltop` | Shows the top 10 bank balances. |

Accepted amount formats:

- Whole numbers: `64`, `1000`, `25000`
- Short numbers: `1k`, `1.5k`, `2m`
- Keywords where supported: `all`, `half`

## Admin Commands

Admin commands use `/emeraldvault` or `/emv`.

| Command | Description |
| --- | --- |
| `/emv help` | Shows admin commands. |
| `/emv reload` | Reloads config/messages and refreshes runtime tasks. |
| `/emv info` | Shows plugin version info. |
| `/emv info <player>` | Shows a player's account info. |
| `/emv add <player> bank <amount>` | Adds money to a player's bank balance. |
| `/emv add <player> savings <amount>` | Adds money to a player's savings balance if savings is unlocked. |
| `/emv remove <player> <amount>` | Removes money from a player's bank balance. |
| `/emv set <player> <amount>` | Sets a player's bank balance. |
| `/emv level <player> <level>` | Sets a player's bank level. |
| `/emv addall <amount>` | Adds money to every account. |
| `/emv removeall <amount>` | Removes money from every account, capped by each player's balance. |
| `/emv resetall PASSWORD` | Resets all player bank data. The password is set in `config.yml`. |
| `/emv db` | Shows transaction count, estimated transaction storage size, and visible history size. |
| `/emv db user <player>` | Shows transaction storage information for one player. |
| `/emv db prune <player>` | Deletes hidden old transactions for one player while keeping visible history. |
| `/emv savings list <player>` | Lists a player's pending savings transfers with numbers. |
| `/emv savings push <player> <number>` | Forces one numbered pending savings transfer to process now. |
| `/emv savings push <player> all` | Forces all pending savings transfers for one player to process now. |
| `/emv savings pushall` | Forces all pending savings transfers for every account to process now. |

## Permissions

| Permission | Default | Description |
| --- | --- | --- |
| `emeraldvault.use` | Everyone | Allows normal player commands. |
| `emeraldvault.admin` | OP | Allows `/emv` admin commands. |
| `emeraldvault.bypass.transferlevel` | OP | Bypasses transfer level requirements. |
| `emeraldvault.*` | OP | Grants all EmeraldVault permissions. |

Bank features are mostly controlled by bank levels and config toggles, not by many separate permission nodes.

## PlaceholderAPI

Identifier: `emv`

PlaceholderAPI support registers automatically when PlaceholderAPI is installed.

| Placeholder | Value |
| --- | --- |
| `%emv_balance%` | Raw bank balance. |
| `%emv_balance_formatted%` | Bank balance with thousands separator. |
| `%emv_balance_short%` | Short bank balance, such as `1.25k`. |
| `%emv_savings%` | Raw savings balance. |
| `%emv_savings_formatted%` | Savings balance with thousands separator. |
| `%emv_savings_short%` | Short savings balance. |
| `%emv_hand%` | Raw valid emerald amount in inventory. |
| `%emv_hand_formatted%` | Hand amount with thousands separator. |
| `%emv_hand_short%` | Short hand amount. |
| `%emv_total%` | Raw bank plus hand amount. |
| `%emv_total_formatted%` | Bank plus hand with thousands separator. |
| `%emv_total_short%` | Short bank plus hand amount. |
| `%emv_bank_cap%` | Raw current bank cap. |
| `%emv_bank_cap_formatted%` | Current bank cap with thousands separator. |
| `%emv_bank_cap_short%` | Short current bank cap. |
| `%emv_savings_cap%` | Raw current savings cap. |
| `%emv_savings_cap_formatted%` | Current savings cap with thousands separator. |
| `%emv_savings_cap_short%` | Short current savings cap. |
| `%emv_bank_level%` | Current bank level. |
| `%emv_bank_level_max%` | Highest configured bank level. |
| `%emv_interest%` | Current online interest rate. |
| `%emv_interest_offline%` | Current offline interest rate. |
| `%emv_next_interest%` | Time until next interest payout, one unit at a time. |
| `%emv_next_interest_seconds%` | Raw seconds until next interest payout. |
| `%emv_auto_deposit%` | `enabled` or `disabled`. |
| `%emv_bank_funded_trades%` | `enabled` or `disabled`. |

Formatted numbers use `formatting.thousands-separator`.
Short numbers use `formatting.compact.decimals` and the configured `k`, `m`, and `b` suffixes.

## Configuration Files

EmeraldVault uses two main config files:

- `config.yml`: economy behavior, levels, caps, interest, database, GUI toggles, formatting.
- `messages.yml`: chat messages and the admin prefix.

### Currency

Currency is emerald-based for version 1.

```yaml
currency:
  bank-verified-items: false
  symbol: "✦"
```

`bank-verified-items: true` means only emeralds withdrawn from EmeraldVault count as valid currency for deposit/spending. Leave it `false` if normal Minecraft emeralds should work.

### World Whitelist

```yaml
world-whitelist:
  enabled: true
  worlds: ['world', 'world_nether', 'world_the_end']
```

When enabled, EmeraldVault only works in listed worlds. Commands, Vault economy calls with a world, and player economy actions are blocked outside the whitelist.

### Bank GUI

```yaml
bank-gui:
  settings-enabled: true
  transaction-history-pages: 3
```

`settings-enabled: false` hides settings from the GUI. Players can still use commands if the feature itself is enabled and unlocked.

### Auto-Deposit

```yaml
auto-deposit:
  enabled: true
  enabled-by-default: true
  player-toggle-allowed: true
```

Auto-deposit moves picked-up emeralds into the bank when the player has the feature enabled and enough bank space. Pickup deposits are grouped for 5 seconds so transaction history does not fill with many single-item pickups.

### Transfers

```yaml
transfers:
  enabled: true
```

Transfers use `/pay` and the transfer GUI. The sender and recipient both need the transfer unlock unless the sender has `emeraldvault.bypass.transferlevel`.

### Savings

```yaml
savings:
  enabled: true
  interest-overflow: SKIP
  transfer-delay-enabled: true
  transfer-delay-hours: 24
  transfer-delay-seconds: 0
```

Savings requires the `INTEREST_ACCOUNT` level unlock. Deposits into savings and withdrawals out of savings can be delayed. Pending savings transfers are not counted as savings balance for interest.

`interest-overflow` controls what happens when interest would exceed savings cap:

- `SKIP`: skip the part that does not fit.
- `PAY_TO_BANK`: pay overflow into the normal bank account.

### Interest

```yaml
interest:
  enabled: true
  payout:
    mode: WEEKLY
    timezone: "UTC"
    day: "FRIDAY"
    hour: 20
    minute: 0
    monthly: LAST_DAY
  required-online-percent: 5.0
  max-payout: 500
```

Interest is paid into savings only. It uses each player's tracked online/offline time and savings balance during the payout window.

Payout modes:

- `HOURLY`: repeats every `hour` + `minute`, for example `1` hour and `30` minutes.
- `DAILY`: pays every day at `hour:minute`.
- `WEEKLY`: pays on `day` at `hour:minute`.
- `MONTHLY`: pays on `FIRST_DAY` or `LAST_DAY` at `hour:minute`.

Players must meet `required-online-percent` during the payout window. Set it to `0` to disable the activity requirement.

### Villager Trading

```yaml
villager-trading:
  bank-funded-inputs:
    enabled: true
    player-toggle-allowed: true
```

When unlocked and enabled, missing emeralds for villager trades can be paid from the player's bank. Shift-click attempts to buy the maximum possible amount. Repeated clicks can fill more emeralds for multiple trades.

### Database

```yaml
database:
  sqlite:
    file: emeraldvault.db
  transaction-pruning:
    enabled: true
    keep-extra-pages: 0
```

EmeraldVault stores account data and history in SQLite. Transaction pruning keeps the database from growing forever by deleting history older than the visible transaction pages plus `keep-extra-pages`.

Admin inspection commands:

- `/emv db`
- `/emv db user <player>`
- `/emv db prune <player>`

### Formatting

```yaml
formatting:
  thousands-separator: "."
  compact:
    decimals: 2
```

Examples with default compact decimals:

- `1000` -> `1k`
- `1359` -> `1.35k`
- `1250000` -> `1.25m`

Set `decimals` to `0`, `1`, or `2`.

## Bank Levels

Levels are configured under `levels`.

Each level can define:

- `bank-cap`
- `savings-cap`
- `online-interest-rate`
- `offline-interest-rate`
- `upgrade-cost-currency`
- `upgrade-cost-items`
- `placeholder-requirements`
- `unlocks`

Unlocks are cumulative, so features unlocked at lower levels stay unlocked at higher levels.

Available unlock names:

| Unlock | Effect |
| --- | --- |
| `DEPOSIT` | Allows deposits. |
| `WITHDRAW` | Allows withdrawals. |
| `BALANCE` | Allows balance checks. |
| `INTEREST` | Allows interest payouts. |
| `TRANSFERS` | Allows `/pay` and GUI transfers. |
| `TRANSACTION_HISTORY` | Allows transaction history GUI. |
| `AUTO_DEPOSIT_TOGGLE` | Allows players to toggle auto-deposit. |
| `INTEREST_ACCOUNT` | Allows the savings account. |
| `BANK_FUNDED_TRADES` | Allows bank-funded villager trades. |

Multi-item upgrade cost example:

```yaml
upgrade-cost-items:
  items: [DIAMOND, NETHER_STAR]
  amounts: [2, 4]
```

This requires 2 diamonds and 4 nether stars.

PlaceholderAPI requirement example:

```yaml
placeholder-requirements:
  placeholders: ["%auraskills_level_fishing%", "%auraskills_level_farming%"]
  display-names: ["Fishing", "Farming"]
  values: [1, 2]
```

This requires Fishing 1 and Farming 2. If PlaceholderAPI is installed, EmeraldVault checks configured placeholders on startup/reload and warns when a placeholder is not found.

Use this to disable item or placeholder requirements for a level:

```yaml
upgrade-cost-items:
  items: ['']
  amounts: [0]
placeholder-requirements:
  placeholders: ['']
  display-names: ['']
  values: [0]
```

## Vault Support

If Vault is installed, EmeraldVault registers itself as a Vault economy provider named `EmeraldVault` with high service priority.

Vault behavior:

- Balance is the normal bank balance, not savings.
- Deposits and withdrawals through Vault are logged in transaction history.
- Fractional currency is not used; values are floored to whole numbers.
- Vault bank APIs are not supported.
- World-aware Vault calls respect the world whitelist.

Interest remains internal to EmeraldVault and is not linked to other economy plugins.

## GUI Features

The bank GUI includes:

- Main bank overview.
- Your Account GUI for deposit, withdraw, and transfer actions.
- Number pad input GUI with quick amounts, max, half, clear, and backspace.
- Bank level GUI with colored level status.
- Savings GUI with pending transfers and interest information.
- Transaction history GUI with filters.
- Transfer GUI listing players with bank accounts.
- Settings GUI for player toggles.

The GUI automatically hides or replaces unavailable features when disabled in config or locked by bank level.

## Transaction History

History tracks the main economy actions, including:

- Deposits
- Withdrawals
- Player transfers
- Savings deposits and withdrawals
- Pending savings transfers
- Interest payouts
- Villager trades funded by the bank
- Vault deposits and withdrawals
- Admin changes

The visible history size is `bank-gui.transaction-history-pages * 28`.

## Messages

All configurable messages are in `messages.yml`.

User-facing messages intentionally do not include the EmeraldVault prefix. Admin and system messages use:

```yaml
messages:
  prefix: "&6✦ &a&lEmerald&6&lVault &8| "
```

Use `&` color codes.

## Config Validation

EmeraldVault validates important config values on startup and reload.

If the config has warnings:

- Console receives the detailed warning lines.
- `/emv reload` only tells the admin `Config error.`
- Admins with `emeraldvault.admin` receive `Config error.` when they join.

Common warnings include invalid materials, mismatched item/amount lists, invalid placeholders, negative values, and invalid schedule options.

## Build

This project uses Maven:

```bash
mvn -q -DskipTests package
```

The current build config writes the jar to:

```text
../test_server/plugins/EmeraldVault.jar
```

## Credits

EmeraldVault by LukasBSR / Cansix.
