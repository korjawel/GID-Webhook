# GID Diablo 2 Item Webhook

Advanced Discord webhook for Diablo 2 Resurrected item tracking using GID loot logs.

Automatically posts item drops to Discord with images, pricing, perfect roll scores, and farming statistics — no code editing required.

---

## Example Output

### Perfect Roll
[![Perfect Roll Example](https://github.com/korjawel/GID-Webhook/raw/main/Screenshots/discord_example_perfect.png)](/korjawel/GID-Webhook/blob/main/Screenshots/discord_example_perfect.png)

### High Rune
[![Rune Example](https://github.com/korjawel/GID-Webhook/raw/main/Screenshots/discord_example_rune.png)](/korjawel/GID-Webhook/blob/main/Screenshots/discord_example_rune.png)

---

## Dashboard Preview

Tracks performance across sessions: runes per hour, deaths, roll tier distribution, zone efficiency and character comparison.

[![Dashboard Example](https://github.com/korjawel/GID-Webhook/raw/main/Screenshots/dashboard_example.png)](/korjawel/GID-Webhook/blob/main/Screenshots/dashboard_example.png)

---

## Features

### Item Detection and Routing

Automatically detects and routes to separate Discord channels:

- Unique items
- Set items
- Runewords
- High Runes
- All other Runes
- Charms
- Jewels
- Rings
- Weapons and Armor
- Keys and Essences
- DLC items (Sling, Dreadfang, Opalvein, Wraithstep, Ars Tor'Baalos, Ars Dul'Mephistos, Ars Al'Diabolos, Gheed's Wager, Entropy Locket, Hellwarden's Will, Measured Wrath, Bloodpact Shard)
- Worldstone Shards
- Statues
- Unidentified items
- Deaths

Items with no configured channel fall back to Default automatically.

---

### Perfect Roll Detection

Rules-based scoring engine covering 400+ items defined in `PerfectRollRules.json`.

Scores each variable stat individually as a percentage of its possible range, then averages across all variable stats to produce a single roll quality percentage.

Roll tiers:

| Tier | Quality |
|---|---|
| Perfect | 100% — every stat at maximum |
| Godly | 99%+ |
| Near Perfect | 95–98% |
| Great Roll | 93–94% |
| Good Roll | 85–92% |
| Average | Below 85% |

Fixed stats (e.g. proc chances, charged skills) are correctly excluded from scoring. Only genuinely variable stats are evaluated.

Example embed:

```
Perfect Roll (100%) – Magefist
Roll Tier: Perfect
Roll Quality: 100%
Perfect Stats Hit:
  ✓ +30% Enhanced Damage
  ✓ 20% Faster Cast Rate
```

---

### Magic Item Type and Image Detection

Items with prefixes and suffixes (magic and rare items) are automatically parsed to extract the base item name before type classification and image lookup.

Examples:
- `Godly Sacred Targe of Deflecting` → type: **Shield**, image: Sacred Targe
- `Master's Circlet of the Magus` → type: **Helm**, image: Circlet
- `Rose Branded Coronet of the Magus` → type: **Helm**, image: Coronet
- `Superior Colossus Voulge` → type: **Weapon**, image: Colossus Voulge

---

### Price Estimation Engine

Combines multiple pricing sources:

- Diablo2.io live market listings
- Traderie marketplace data
- ConsultantPro price reference
- Curated price catalogs (runes, runewords, uniques, charms, bases)
- Synthetic fallback estimation for items with no live data

Produces per-item output:

```
Estimated Value: 75 FG (40–120)
Confidence: Medium | Samples: 12 | Trend: +5%
Source: Diablo2IO live market
```

Run `Update-PriceCache.ps1` before first use to build the local cache.

---

### Dashboard System

Automatically generated performance files updated in real time:

| File | Contents |
|---|---|
| `dashboard.html` | Visual dashboard — open in browser, refresh to update |
| `dashboard_drops.csv` | Full drop history |
| `dashboard_graph.json` | Hourly drop rate graph data |
| `dashboard_summary.txt` | Plain text stats summary |

Tracks: items per hour, high rune frequency, deaths, roll tier distribution, zone scores, character efficiency, session comparison.

---

### Scheduled Summaries

Posts automatic summary embeds to Discord on a configurable schedule:

- **Daily summary** — posted at a configured hour each day
- **Weekly summary** — posted on a configured day and hour each week
- **Session dashboard** — posted automatically when the script restarts, summarising the previous session

Summaries include: items/hour, high runes, deaths, top farming zones, recent perfect rolls, and a per-character efficiency breakdown.

---

### Statistics Tracking

Persistent statistics stored in `statistics.json`:

- Lifetime totals (items, HR, deaths, uniques, sets)
- Daily and weekly breakdowns
- Per-character stats (items, HR, deaths, perfect rolls, near-perfects)
- High rune location heatmap
- Roll history with tier distribution
- Unique grail tracker
- Streak tracking (runs since last HR, longest dry spell)
- RNG luck score (actual vs expected high runes)

---

### Config Driven

All personal settings live in `UserConfig.psd1`. The main script is never edited directly.

This means:
- Upgrading is safe — just replace the script files, keep `UserConfig.psd1`
- Settings are portable — easy to share or back up
- Zero reconfiguration needed on updates

---

## Requirements

**PowerShell 7** (not Windows PowerShell 5)

Download: https://github.com/PowerShell/PowerShell/releases

Install the `.msi` file for Windows. Test with:

```
pwsh
```

A blue window showing `7.x` means you are ready.

---

## Installation

### 1. Download

Download the ZIP from GitHub or clone the repo:

```
git clone https://github.com/korjawel/GID-Webhook
```

### 2. Configure Webhooks

[![Config Example](https://github.com/korjawel/GID-Webhook/raw/main/Screenshots/edit_script_webhook.png)](/korjawel/GID-Webhook/blob/main/Screenshots/edit_script_webhook.png)

Open `UserConfig.psd1` and add your Discord webhook URLs:

```powershell
Webhooks = @{
    Default          = "https://discord.com/api/webhooks/..."
    HighRunes        = "https://discord.com/api/webhooks/..."
    Runes            = "https://discord.com/api/webhooks/..."
    Uniques          = "https://discord.com/api/webhooks/..."
    Sets             = "https://discord.com/api/webhooks/..."
    Charms           = "https://discord.com/api/webhooks/..."
    Jewels           = "https://discord.com/api/webhooks/..."
    Ring             = "https://discord.com/api/webhooks/..."
    Weapons          = "https://discord.com/api/webhooks/..."
    Armor            = "https://discord.com/api/webhooks/..."
    Keys             = "https://discord.com/api/webhooks/..."
    Essences         = "https://discord.com/api/webhooks/..."
    Runewords        = "https://discord.com/api/webhooks/..."
    DLC              = "https://discord.com/api/webhooks/..."
    Shards           = "https://discord.com/api/webhooks/..."
    Statues          = "https://discord.com/api/webhooks/..."
    Deaths           = "https://discord.com/api/webhooks/..."
    DailySummary     = "https://discord.com/api/webhooks/..."
    WeeklySummary    = "https://discord.com/api/webhooks/..."
    SessionDashboard = "https://discord.com/api/webhooks/..."
    Muled            = "https://discord.com/api/webhooks/..."
}
```

Unused channels fall back to `Default` automatically. You do not need all channels.

### 3. Configure GID Paths

```powershell
Paths = @{
    LootFolder = "C:\GID\Looted"
    LogsFolder = "C:\GID\Logs"
}
```

`LootFolder` — parent folder containing your bot character subfolders (each should contain a `Looted.log`)  
`LogsFolder` — folder containing your GID session log `.txt` files

### 4. Set Your Timezone

```powershell
TimezoneOffsetHours = 0
```

Set to your UTC offset. This is used to correctly match item drop timestamps to bot log files for location detection.

| Timezone | Standard | Daylight Saving |
|---|---|---|
| New Zealand | 12 | 13 (Oct–Apr) |
| Australian Eastern | 10 | 11 (Oct–Apr) |
| US Eastern | -5 | -4 (Mar–Nov) |
| US Central | -6 | -5 (Mar–Nov) |
| US Pacific | -8 | -7 (Mar–Nov) |
| UK | 0 | 1 (Mar–Oct) |
| Central European | 1 | 2 (Mar–Oct) |

### 5. Build Price Cache (Required)

Run once before first use:

```
pwsh -ExecutionPolicy Bypass -File .\Update-PriceCache.ps1
```

Builds the pricing lookup database. First run takes 10–20 minutes. Only needs to be re-run when price sources are updated or the cache is deleted.

### 6. Run the Webhook

[![Run Script](https://github.com/korjawel/GID-Webhook/raw/main/Screenshots/powershell_run.png)](/korjawel/GID-Webhook/blob/main/Screenshots/powershell_run.png)

```
pwsh -ExecutionPolicy Bypass -File .\Webhook.ps1
```

Leave the window open. The script monitors your GID folders continuously.

### 7. Start GID

Items will post to Discord automatically as they drop.

---

## Folder Structure

[![Folder Structure](https://github.com/korjawel/GID-Webhook/raw/main/Screenshots/folder_structure.png)](/korjawel/GID-Webhook/blob/main/Screenshots/folder_structure.png)

```
GID-Webhook/
├── Images/                          Game item images for Discord embeds
├── Logs/                            Auto-generated error and image logs
├── Screenshots/                     Auto-generated screenshots (if enabled)
├── Tools/                           Utility tools
│
├── Webhook.ps1                      Main monitoring script  ← replace on update
├── Update-PriceCache.ps1            Price cache builder     ← replace on update
├── UserConfig.psd1                  Your personal config    ← KEEP on update
│
├── PerfectRollRules.json            Roll scoring rules      ← replace on update
├── SetItems.json                    Set item database       ← replace on update
├── UniqueItems.json                 Unique item database    ← replace on update
├── RarityLookup.csv                 Rarity classification   ← replace on update
├── gfx.csv                          Image code mapping      ← replace on update
│
├── price_catalog_*.json             Pricing catalogs        ← replace on update
├── price_aliases.json               Price name aliases      ← replace on update
├── price_sources.json               Price source config     ← replace on update
├── price_overrides.json             Manual price overrides  ← replace on update
│
├── consultantpro_price_cache.json   Auto-generated — do not share
├── statistics.json                  Auto-generated — do not share
├── PerfectRolls.json                Auto-generated — do not share
├── dashboard.html                   Auto-generated — do not share
└── itemlog.csv / itemlog_YYYY-MM.csv Auto-generated — do not share
```

---

## Updating to a New Version

Replace these files with the new versions:

```
Webhook.ps1
Update-PriceCache.ps1
PerfectRollRules.json
SetItems.json
UniqueItems.json
RarityLookup.csv
gfx.csv
All price_catalog_*.json files
price_aliases.json
price_sources.json
price_overrides.json
```

Keep this file — your settings are preserved:

```
UserConfig.psd1
```

You do **not** need to reconfigure anything when updating.

---

## Optional UserConfig.psd1 Settings

### DebugLogging

```powershell
DebugLogging = $false
```

Set to `$true` to enable verbose console output per item. Useful for troubleshooting location detection, type classification, or image lookup. Leave `$false` during normal farming sessions.

### HighRunes Threshold

```powershell
HighRunes = @(
    "Ist", "Gul", "Vex", "Ohm", "Lo",
    "Sur", "Ber", "Jah", "Cham", "Zod"
)
```

Remove runes from the top of the list to raise the threshold. Items matching this list route to the `HighRunes` channel and count toward high rune statistics.

### Mule Character

```powershell
MuledConfig = @{
    CharacterName       = "MyMuleCharacter"
    ChannelName         = "Muled"
    BatchSize           = 8
    PauseBetweenItems   = 1.5
    PauseBetweenBatches = 6
}
```

Items from this character are posted to the Muled channel in batches but excluded from statistics to avoid double-counting.

### Summary Schedule

```powershell
SummaryConfig = @{
    DailyHour  = 8     # Hour of day to post daily summary (0-23)
    WeeklyDay  = 0     # 0=Sunday, 1=Monday ... 6=Saturday
    WeeklyHour = 20    # Hour of day to post weekly summary (0-23)
}
```

All times are in your local timezone as set by `TimezoneOffsetHours`.

---

## Creating Discord Webhooks

[![Create Webhook](https://github.com/korjawel/GID-Webhook/raw/main/Screenshots/webhook_create.png)](/korjawel/GID-Webhook/blob/main/Screenshots/webhook_create.png)

1. Open Discord
2. Right click a channel → **Edit Channel**
3. **Integrations** → **Webhooks** → **Create Webhook**
4. Copy the webhook URL
5. Paste into `UserConfig.psd1`

![Create Webhook](Screenshots/webhook_create.png)

---

## Troubleshooting

**Nothing is posting**
- Check webhook URLs in `UserConfig.psd1`
- Check GID folder paths in `UserConfig.psd1`
- Confirm PowerShell 7 is installed (`pwsh --version`)
- Confirm price cache was built successfully (`Update-PriceCache.ps1`)

**Items showing `Type: Unknown` or wrong image**
- Ensure you are on v4.1 or later — magic/rare items with prefixes and suffixes (e.g. `Godly Sacred Targe of Deflecting`) are now handled automatically

**Location showing `Unknown`**
- Check `TimezoneOffsetHours` in `UserConfig.psd1` matches your actual local timezone

**Perfect roll showing 100% but stats listed as missing**
- Ensure you are on v4.1 or later — a clamping bug affecting items with `Defense` stats (Toothrow, Duskdeep, Leviathan, Venom Grip, Crown of Ages) was fixed

**Price not showing**
- Run `Update-PriceCache.ps1` to refresh the price cache

**Log files for errors:**
```
Logs\script_errors.txt
Logs\monitor_errors.txt
Logs\imagelog.txt
```

---

## Technical Notes

- `statistics.json` is written once per monitoring cycle (every 5 seconds) rather than after every item, reducing disk I/O
- Each `Looted.log` is read once per cycle rather than twice per item
- Discord 429 rate limit responses are handled automatically with retry using the Discord-provided `retry_after` delay
- `itemlog.csv` is automatically archived monthly to `itemlog_YYYY-MM.csv`
- `statistics.json` arrays are trimmed to 90 days of detail after sustained use to prevent unbounded file growth

---

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md)

---

## License

MIT License
