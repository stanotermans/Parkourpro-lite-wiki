# Pumpkin edition

ParkourPro Lite is also available for [Pumpkin](https://pumpkinmc.org/), the Minecraft server written in Rust. It is a separate, native build: the Spigot/Paper jar does not run on Pumpkin.

> The Pumpkin edition has its own commands, permissions and settings. Everything that applies to it is on this page; the other pages describe the Spigot/Paper editions.

## Installation

1. Download the `.wasm` file from the [Pumpkin Market](https://market.pumpkinmc.org/). Pick the file that matches your Pumpkin version.
2. Put it in the `plugins/` folder of your Pumpkin server and start the server.
3. On first start Pumpkin asks to allow `fs.write.data`. The plugin needs it to save parkours, records and settings in its own data folder. Answer `y`.
4. Set `language` in `config.yml` (for example `nl_NL`) and run `/parkour reload`.

| Component | Supported |
|---|---|
| Server software | Pumpkin 0.2.0 |
| Minecraft | 26.3 |
| Plugin version | 1.1.0 |

A plugin only loads on the Pumpkin version it was built for. After updating Pumpkin, download the matching plugin file again. The error "Plugin is built against a different API version" means the file and the server do not match.

## Your first parkour

1. Place a **gold pressure plate** (light weighted), look at it or stand on it and run `/parkour setstart <name>`.
2. Place a second gold pressure plate and run `/parkour setend <name>`.
3. Place **iron pressure plates** (heavy weighted) and run `/parkour addcheckpoint <name>` for each one, in course order.
4. Stand where you want the leaderboard and run `/parkour addleaderboard <name>`.

Step on the start plate to begin. Your inventory is emptied during the run and given back when you finish, cancel or leave.

## Commands

Root command `/parkour`, aliases `/pk` and `/par`.

| Command | Permission | What it does |
|---|---|---|
| `/parkour checkpoint` | use | Teleports you to your last checkpoint. |
| `/parkour reset` | use | Back to the reset location, timer restarts. |
| `/parkour cancel`, `/parkour leave` | use | Ends your run. |
| `/parkour list` | use | Lists all parkours. |
| `/parkour top <parkour> [page]` | use | Best times of a parkour. |
| `/parkour pb <parkour> [player]` | use | Personal best, statistics and checkpoint splits. |
| `/parkour version` | use | Shows the plugin version. |
| `/parkour setstart <name>` | admin | Sets the start plate (gold). Creates the parkour. |
| `/parkour setend <name>` | admin | Sets the finish plate (gold). |
| `/parkour addcheckpoint <name>` | admin | Adds the iron plate as the next checkpoint. |
| `/parkour deletecheckpoint <name> <number>` | admin | Removes a checkpoint. |
| `/parkour setreset <name>` | admin | Sets the reset location to where you stand. |
| `/parkour setleaveposition <name>` | admin | Where players go when they leave or cancel. |
| `/parkour delete <name>` | admin | Deletes the parkour. |
| `/parkour addleaderboard <name>` | admin | Places the leaderboard hologram where you stand. |
| `/parkour setleaderboardsize <name> <size>` | admin | Number of places on the leaderboard. |
| `/parkour sethologram <name> <start\|end\|checkpoint> <text>` | admin | Custom hologram text, `\|` starts a new line. `default` restores the text from config.yml. |
| `/parkour setfallback <name> <y\|off>` | admin | Players below this height are sent back. |
| `/parkour setcooldown <name> <seconds>` | admin | Waiting time after finishing, 0 = off. |
| `/parkour setmaxattempts <name> <perDay>` | admin | Attempts per player per day, 0 = unlimited. |
| `/parkour setleaveradius <name> <blocks>` | admin | Cancels the run when the player moves this far from the course, 0 = off. |
| `/parkour deletetime <parkour> <player>` | admin | Deletes a record. |
| `/parkour settime <parkour> <player> <mm:ss.ms>` | admin | Sets a record, for example `01:23.456`. |
| `/parkour reload` | admin | Reloads config.yml, the language and all holograms. |

## Permissions

Pumpkin requires permission nodes to start with the plugin name, so they differ from the Spigot/Paper editions.

| Node | Default | Grants |
|---|---|---|
| `parkourpro-lite:use` | everyone | Running parkours and the player commands. |
| `parkourpro-lite:admin` | op (level 2) | Creating and managing parkours, records and reload. |

## Configuration and languages

`config.yml` uses the same layout and names as the Spigot/Paper edition, so the [Configuration](Configuration) page applies to the sections below. All 23 languages are included in the `languages/` folder.

| Section | Notes for Pumpkin |
|---|---|
| `language` | Same as Spigot/Paper. |
| `sounds` | Use Minecraft sound names such as `block.note_block.pling`. Empty = no sound. |
| `checkpoints.sequential` | Same as Spigot/Paper. |
| `timer-display` | `type` is `actionbar` or `disabled`. |
| `bed-confirmation` | Same as Spigot/Paper. |
| `fallback` | `default-y` is applied to newly created parkours when `y-enabled` is true. |
| `holograms` | Text, leaderboard format, colours and offsets. A hologram grows upwards from its base, so the offsets are the height of the bottom line. |
| `items` | Material, name, slot and click type of the three hotbar items. `items.enabled: false` keeps the inventory untouched. |
| `leave.teleport-to` | `start`, `reset` or `none`. |
| `broadcast.record` | Same as Spigot/Paper. |
| `features.restart-on-same-start` | Same as Spigot/Paper. |

## Files

| File | Contents |
|---|---|
| `config.yml` | Settings. |
| `languages/*.yml` | Messages per language. Add your own file and set its name as `language`. |
| `parkours.json` | Parkours, checkpoints and rules. |
| `records.json` | Best times and checkpoint splits. |
| `stats.json` | Attempts, completions and play time per player. |

## Not available on Pumpkin yet!

- All [Pro features](Pro-Features): there is no Pro edition for Pumpkin yet.
- End and reward commands, MySQL, the Discord webhook, PlaceholderAPI placeholders and the update checker.
- Anti-cheat checks, parkour locks, death handling, custom sounds and titles per parkour, import and export, the creation wizard.
- Title and boss bar timers, and rank prefixes on the leaderboard.

## Known issues

- **Ghost items in the crafting grid.** During a run two of the parkour items can also appear in the crafting slots of the inventory screen. They are only visible on the client and disappear when clicked. This is caused by Pumpkin 0.2.0 and cannot be fixed by the plugin.
- **Server crash during a run.** The inventory of a running player is kept in memory. It is given back on finish, cancel, leave, disconnect and a normal server stop, but not after a crash.
