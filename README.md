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
