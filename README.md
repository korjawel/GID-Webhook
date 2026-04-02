# GID Diablo 2 Item Webhook

Advanced Discord webhook for Diablo 2 Resurrected item tracking using GID loot logs.

Provides:

• automatic item posting  
• perfect roll detection  
• price estimation  
• multi-channel routing  
• dashboard tracking  
• runeword detection  
• DLC item support  
• superior item gfx detection  

---

# Features

## Item Detection
Automatically detects:

• Unique items  
• Set items  
• Runewords  
• Runes  
• Charms  
• Jewels  
• Rings  
• Amulets  
• Bases  
• Keys  
• Essences  
• DLC items  

---

## Perfect Roll Detection

Uses configurable rules:

PerfectRollRules.json

Supports:

• weighted stat scoring  
• variable stat ranges  
• stat direction preference  
• multi-stat evaluation  

Roll tiers:

Perfect  
Godly  
Great  
Good  
Average  
Low  

Example output:

Perfect Roll (100%) – Magefist

---

## Price Estimation Engine

Combines multiple price sources:

• Diablo2.io listings  
• curated price datasets  
• rune normalization  
• runeword valuation logic  
• synthetic fallback estimation  

Produces:

Estimated value  
confidence rating  
sample size  

Example:

Estimated Value: 75 FG (40–120)  
Confidence: Medium  

---

## Config Driven Setup

All personal configuration stored in:

UserConfig.psd1

Allows:

easy upgrades  
safe sharing  
multi-user support  
no script editing required  

---

## Dashboard Tracking

Tracks performance across sessions:

dashboard_drops.csv  
dashboard_summary.txt  
dashboard_graph.json  

Supports:

session stats  
daily totals  
 lifetime totals  
 drop frequency  

---

## Superior Item Handling

Superior bases automatically normalized:

Superior Archon Plate → Archon Plate

Ensures correct image detection and avoids fallback gfx.

---

## DLC Item Support

Supports custom expansion items:

Entropy Locket  
Horazon items  
Worldstone Shard items  
custom mod items  

Routes automatically to DLC webhook channel.

---

# Requirements

PowerShell 7

Download:
https://github.com/PowerShell/PowerShell/releases

---

# Installation

## Step 1 – Download release

Download repo zip or clone repo.

---

## Step 2 – Configure User Settings

Open:

UserConfig.psd1

Configure:

Webhook URLs
GID folder paths

Example:

Webhooks = @{
Default = ""
Runes = ""
Uniques = ""
Sets = ""
Charms = ""
Jewels = ""
Rings = ""
Amulets = ""
Armor = ""
Weapons = ""
Runewords = ""
Essences = ""
DLC = ""
}

Paths = @{
LootFolder = "C:\GID\Looted"
LogsFolder = "C:\GID\Logs"
}

---

## Step 3 – Build Price Cache

Required before first run.

Run:

pwsh -ExecutionPolicy Bypass -File .\Update-PriceCache.ps1

This prepares local pricing database.

May take 10–20 minutes on first run.

Only required when:

price sources updated
fresh install
cache deleted

---

## Step 4 – Run Webhook

Run:

pwsh -ExecutionPolicy Bypass -File .\Webhook.ps1

Leave PowerShell window open.

---

## Step 5 – Start GID

Items will begin posting automatically.

---

# File Structure

Webhook.ps1  
Update-PriceCache.ps1  
UserConfig.psd1  

PerfectRollRules.json  
PerfectRolls.json  

UniqueItems.json  
SetItems.json  

price_catalog_*.json  
price_sources.json  

gfx.csv  
RarityLookup.csv  

Images/  
Logs/  
Screenshots/  

---

# Updating Script

When updating:

replace:

Webhook.ps1  
Update-PriceCache.ps1  
PerfectRollRules.json  
pricing json files  

keep:

UserConfig.psd1  

---

# Troubleshooting

Nothing posting:

check webhook URL
check folder paths
check PowerShell version
check logs folder

Logs:

Logs/script_errors.txt  
Logs/monitor_errors.txt  
Logs/imagelog.txt  

---

# Advanced Features

## Multi-channel routing

Supports routing by:

item type  
rarity  
runeword  
perfect roll tier  

---

## Confidence scoring

Price confidence calculated using:

sample size
source consistency
price variance
synthetic fallback usage

---

## Synthetic price fallback

Used when live price unavailable.

Ensures all items have approximate value.

---

## Alias normalization

Handles name variations:

Shako → Harlequin Crest  
SoJ → Stone of Jordan  

---

# Contributing

See contributor guide below.

---

# License

MIT License
