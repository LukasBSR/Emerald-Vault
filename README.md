# Emerald Vault
EmeraldVault is a Minecraft plugin inspired by [BankPlus](https://www.spigotmc.org/resources/%E2%9C%A8-bankplus-%E2%9C%A8.93130/) and [The Emerald Bank](https://www.spigotmc.org/resources/the-emerald-bank.71210/). It allows players to securely deposit and withdraw emeralds in a virtual bank, providing a safe way to manage their wealth in a survival server.

**[Vault](https://www.spigotmc.org/resources/vault.34315/) is needed**

**Supportet Verions:** `1.20.4` `1.20.6` `1.21`
*Older versions are not tested, so it might work

## Features
- Withdraw & Deposit Emeralds from and into your Inventory
- use any item as your currency
- Level up your bank to unlock and improve Interest rates and higher bank caps (config.yml)
- Transfer balance to other Players
- Online & Offline Interest (config.yml)
- Auto-deposit feature for mined or gained emeralds
- Bank GUI (config.yml)
- Banktop (config.yml)
- Customizable bank messages and alerts
- Admin commands for managing player balances and bank settings

## Commands
Commands  | Description |
| ------------- | ------------- |
| `/balane`  | sends a message of the players current balance  |
| `/bank`  | opens the bank GUI  |
| `/deposit [all / half / ammount]`  | Deposit into bank (Using /deposit will deposit only the emeralds in the player's hand.) |
| `/withdraw [all / half / ammount]`  | withdraw into players inventory (If there is no space in the inventory, the emeralds will drop  on the ground.) |
| `/transfer <player> <ammount>`  | Transfer Emeralds in the bank to another Player  |
| `/interest`  | View the time left for the interest  |
| `/baltop`  | List the top bank balances  |

Admin Commands  | Description |
| ------------- | ------------- |
| `/bank reload`  | Reloads Config  |
| `/bank add <player> <ammount>`  | add amount of emerald to player balance  |
| `/bank remove <player> <ammount>`  | remove amount of emerald from player balance  |
| `/bank set <player> <ammount>`  | set player's balance  |
| `/bank addall <ammount>`  | add Emeralds to every existing Bank account  |
| `/bank removeall <ammount>`  | remove Emeralds from every existing Bank account  |
| `/bank resetall`  | reset all playerdata.  |
| `/bank level <player> <level>`  | sets the bank level of a player  |



## Placeholders
 Placeholder  | Description |
| ------------- | ------------- |
| `%ev_balance%`  | Total Balance, Hand + bank  |
| `%ev_balance_bank%`  | Only Bank Balance  |
| `%ev_balance_hand%`  | Only inventory balance  |
| `%ev_balance_bank_formatted%`  | Bank Balance formatted (Format in config.yml)  |
| `%ev_balance_hand_formatted%`  | inventory balance formatted (Format in config.yml)  |
| `%ev_bank_level%`  | Bank Level  |
| `%ev_interest%`  | Interest rate  |
| `%ev_next_interest%`  | Time until next Interest rate  |
| `%ev_interest_offline%`  | Interest rate while Offline  |
