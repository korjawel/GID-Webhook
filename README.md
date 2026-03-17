# Diablo II Resurrected – GID Discord Drop Tracker

A real-time Discord notification system for GID / D2RB bots.

This script monitors your GID bot log files and automatically posts item drops to Discord with:

- Item images
- Drop location
- Character name
- Roll quality detection
- Perfect item tracking
- Farming statistics dashboard
- Session dashboard summaries
- Local image fallback support
- Config-based setup that survives future script updates

---

## Example Discord Notifications

### Perfect Item
![Perfect Item](Screenshots/perfect-item.png)

### Rune Drop
![Rune Drop](Screenshots/rune-drop.png)

### Farming Statistics Dashboard
![Dashboard](Screenshots/dashboard.png)

The script automatically builds a dashboard showing:

- Items per hour
- Rune drop history
- Farming zone performance
- Character efficiency
- Perfect roll tracking
- Daily, weekly, and session summaries

---

## Folder Structure

Your folder should look like this:

```text
WebhookWithImages/
│
├── WebhookWithImages.ps1
├── UserConfig.psd1
│
├── PerfectRollRules.json
├── PerfectRolls.json
├── UniqueItems.json
├── SetItems.json
├── RarityLookup.csv
├── gfx.csv
│
├── Images/
├── Logs/
├── Screenshots/
├── Tools/
│
├── README.md
└── QUICKSTART.txt
```

> **Important:**  
> Do not put your personal webhook URLs or local paths into the main `.ps1` script.  
> Put all personal settings in `UserConfig.psd1`.

---

## Requirements

You must install these first.

### 1. Install PowerShell 7

Download the Windows installer from the PowerShell releases page:

```text
https://github.com/PowerShell/PowerShell/releases
```

Install the `.msi` version like any normal program.

### Verify installation

Press:

```text
Windows Key + R
```

Type:

```text
pwsh
```

Press Enter.

You should see a blue PowerShell window showing version 7.x.

---

## 2. Create a Discord Webhook

Open Discord.

Right click the channel you want item drops in.

Click:

```text
Edit Channel
Integrations
Webhooks
New Webhook
```

Copy the webhook URL.

---

## 3. Unblock the Script (Important)

Windows may block downloaded scripts.

Right click:

```text
WebhookWithImages.ps1
```

Click:

```text
Properties
```

At the bottom, check:

```text
Unblock
```

Click **OK**.

You may also want to repeat this for:

- `UserConfig.psd1`
- `PerfectRollRules.json`

---

## 4. Configure the Tracker (New Config Method)

You no longer need to edit personal settings inside the main script.

Open:

```text
UserConfig.psd1
```

This file stores:

- Discord webhook URLs
- GID folder paths
- High rune threshold
- Enabled/disabled channels
- Summary settings
- Muled settings

This means you only set it up once.

When a new script version is released, you normally keep your existing `UserConfig.psd1` and replace only the `.ps1` file.

---

## 5. Add Your Webhooks

Inside `UserConfig.psd1`, find:

```powershell
Webhooks = @{
```

Paste your webhook URLs there.

### Basic one-webhook setup

If you want everything to go to one Discord channel, fill only:

```powershell
Default = "PASTE_WEBHOOK_URL_HERE"
```

### Multi-channel setup

You can also split posts by category, for example:

- `Runes`
- `HighRunes`
- `Uniques`
- `Sets`
- `Runewords`
- `Charms`
- `Jewels`
- `Essences`
- `Keys`
- `DailySummary`
- `WeeklySummary`
- `SessionDashboard`
- `Muled`

If a category is left blank or set to a placeholder, the script will use fallback behavior where applicable.

---

## 6. Configure Your GID Folder Paths

Inside `UserConfig.psd1`, find:

```powershell
Paths = @{
```

Set your folders like this:

```powershell
Paths = @{
    LootFolder = "C:\Users\YourName\Desktop\GID-v3.317\D2RB\Looted"
    LogsFolder = "C:\Users\YourName\Desktop\GID-v3.317\D2RB\Logs"
}
```

If these paths are wrong, the script will not detect items.

---

## 7. Choose Your High Rune Threshold

Inside `UserConfig.psd1`, find:

```powershell
HighRunes = @(
```

Example: record **Ist and above only**

```powershell
HighRunes = @(
    "Ist",
    "Gul",
    "Vex",
    "Ohm",
    "Lo",
    "Sur",
    "Ber",
    "Jah",
    "Cham",
    "Zod"
)
```

Example: record **Pul and above**

```powershell
HighRunes = @(
    "Pul",
    "Um",
    "Mal",
    "Ist",
    "Gul",
    "Vex",
    "Ohm",
    "Lo",
    "Sur",
    "Ber",
    "Jah",
    "Cham",
    "Zod"
)
```

---

## 8. Optional Settings

You can also edit these in `UserConfig.psd1`:

### ChannelsEnabled
Turn specific channels on or off.

### SummaryConfig
Control daily and weekly summary timing.

### MuledConfig
Set character name, batch size, and delays for muled posts.

---

## 9. Run the Script

Open PowerShell 7 in the script folder and run:

```powershell
pwsh -NoProfile -ExecutionPolicy Bypass -File ".\WebhookWithImages.ps1"
```

Leave the window open while your bots are running.

---

## 10. Start GID

Once items drop, they will automatically appear in Discord.

---

## Updating to a New Script Version

This project now supports **config-based upgrades**.

### Normal update process

1. Back up your current folder.
2. Replace `WebhookWithImages.ps1` with the new version.
3. Keep your existing `UserConfig.psd1`.
4. Run the script again.

### Usually you do **not** need to re-enter:

- Webhook URLs
- GID paths
- High rune settings
- Channel preferences

### Important note

If a future update adds a **new config option**, you may need to copy one or two new keys into your existing `UserConfig.psd1`.

That is usually much easier than re-editing the full script every update.

---

## Local Images

The script supports local item images from the `Images` folder.

### Naming rule

Image files should use the cleaned item name plus `_graphic.png`.

Examples:

```text
stormshield_graphic.png
andarielsvisage_graphic.png
trangoulsclaws_graphic.png
mageplate_graphic.png
```

### Important notes

- Use lowercase
- Remove spaces
- Remove apostrophes
- Remove hyphens
- Remove punctuation

### Superior items

For superior base items, the script strips the `Superior` prefix when matching images and item types.

Example:

```text
Superior Mage Plate -> mageplate_graphic.png
```

If no exact item-name image is found, the script can fall back to type-based images.

---

## Troubleshooting

If nothing posts, check:

- PowerShell 7 is installed
- Your webhook URL is correct in `UserConfig.psd1`
- Your `LootFolder` path is correct
- Your `LogsFolder` path is correct
- The script window is still open
- Discord webhooks are allowed in the target channel

### If images do not match

Check that the PNG filename matches the cleaned item name exactly.

### If roll quality looks wrong

Make sure you are using the latest `PerfectRollRules.json`.

### If essences or special items post to the wrong channel

Make sure you are using the latest script version, since routing logic can change between releases.

---

## Files You Should Normally Keep Private

Do not share your personal version of:

- `UserConfig.psd1`
- live logs
- personal statistics files
- any script copy that still contains real webhook URLs

If you want to share the project with others, share the script with placeholders only.

---

## Quick Start

See:

```text
QUICKSTART.txt
```

for the short setup version.

---

## Notes for Future Updates

When new versions are released:

- replace the main script
- keep your config
- review release notes for any new config keys
- update supporting JSON files if the release includes them

This keeps upgrades much faster and safer than editing the whole script every time.
