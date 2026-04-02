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

# Example Output

### Perfect roll example
![Perfect Roll Example](Screenshots/discord_example_perfect.png)

### Rune example
![Rune Example](Screenshots/discord_example_rune.png)

---

# Dashboard Preview

Tracks performance across sessions including runes, deaths, drops per hour and roll tier distribution.

![Dashboard Example](Screenshots/dashboard_example.png)

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

Routes items to correct Discord channels automatically.

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

## Dashboard System

The webhook includes a built-in performance dashboard.

Tracks:

• items per hour  
• rune frequency  
• high rune drops  
• deaths  
• roll tier distribution  
• character activity  
• session duration  

Dashboard files generated automatically:

dashboard.html  
dashboard_drops.csv  
dashboard_graph.json  
dashboard_summary.txt  

Open dashboard.html in browser.

Refresh page to update stats.

Useful for:

tracking farming efficiency  
comparing sessions  
monitoring multiple bots  

---

## Superior Item Handling

Superior bases normalized before image lookup.

Example:

Superior Archon Plate → Archon Plate

Prevents incorrect fallback images.

---

## DLC Item Support

Supports custom expansion items:

Entropy Locket  
Horazon items  
Worldstone Shard items  
custom mod items  

Routes automatically to DLC webhook channel.

---

## Config Driven Setup

All user configuration stored in:

UserConfig.psd1

Allows:

safe upgrades  
easy sharing  
no script editing required  

---

# Requirements

PowerShell 7

Download:

https://github.com/PowerShell/PowerShell/releases

---

# Installation

## 1. Download repo

Download ZIP or clone repo.

---

## 2. Configure Webhooks

Open:

UserConfig.psd1

Add webhook URLs.

Example:

Webhooks = @{
Default = ""
Runes = ""
HighRunes = ""
Uniques = ""
Sets = ""
Charms = ""
Jewels = ""
Rings = ""
Amulets = ""
Weapons = ""
Armor = ""
Runewords = ""
Keys = ""
Essences = ""
DLC = ""
DailySummary = ""
WeeklySummary = ""
Deaths = ""
}

Leave unused channels blank.

They will fallback to Default.

---

## 3. Configure GID Paths

Inside UserConfig.psd1:

Paths = @{
LootFolder = "C:\GID\Looted"
LogsFolder = "C:\GID\Logs"
}

These must match GID output folders.

---

## 4. Build Price Cache (Required)

Run once before first use:

pwsh -ExecutionPolicy Bypass -File .\Update-PriceCache.ps1

Builds pricing lookup database.

First run may take:

10–20 minutes

Required for:

price estimation  
confidence scoring  
rune values  

---

## 5. Run Webhook

Run:

pwsh -ExecutionPolicy Bypass -File .\Webhook.ps1

Leave window open.

---

## 6. Start GID

Items will automatically post to Discord.

---

# Folder Structure

![Folder Structure](Screenshots/folder_structure.png)

Core files:

Webhook.ps1  
Update-PriceCache.ps1  
UserConfig.psd1  

PerfectRollRules.json  

pricing json files  

gfx.csv  
RarityLookup.csv  

Folders:

Images  
Logs  
Screenshots  
Tools  

---

# Creating Discord Webhooks

![Create Webhook](Screenshots/webhook_create.png)

Recommended channel structure:

Default  
high-runes  
runes  
uniques  
sets  
charms  
jewels  
ring  
weapons  
armor  
keys  
essences  
dlc-items  
summaries  

---

# Running Script

![Run Script](Screenshots/powershell_run.png)

Command:

pwsh -ExecutionPolicy Bypass -File .\Webhook.ps1

---

# Editing Config

![Config Example](Screenshots/edit_script_webhook.png)

Edit:

UserConfig.psd1

Do NOT edit main script.

---

# Dashboard Files

dashboard_drops.csv

contains drop history

dashboard_summary.txt

quick stats summary

dashboard_graph.json

graph data

dashboard.html

visual dashboard

---

# Updating Script

Replace:

Webhook.ps1  
Update-PriceCache.ps1  
PerfectRollRules.json  
pricing json files  

Keep:

UserConfig.psd1

---

# Troubleshooting

Nothing posting:

check webhook URL  
check folder paths  
check PowerShell version  
run Update-PriceCache.ps1  

Check logs:

Logs/script_errors.txt  
Logs/monitor_errors.txt  
Logs/imagelog.txt  

---

# Advanced Features

Multi-channel routing

Confidence scoring

Synthetic fallback pricing

Alias normalization

Runeword detection

Perfect roll scoring

Session tracking

Superior base detection

---

# Contributing

See CONTRIBUTING.md

---

# License

MIT License
