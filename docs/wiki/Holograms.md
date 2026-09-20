# Holograms

Every parkour can show a **start**, **end**, per-**checkpoint** and **leaderboard** hologram. Pro adds **daily / weekly / monthly** leaderboards.

## Renderers

| Version | Renderer |
|---|---|
| 1.8 – 1.19 | Invisible armor stands, one per line |
| 1.19.4+ Paper | Text displays; Pro can style them with `sethologramdisplay` |
| 1.20+ Pro | Optional HologramLib renderer (`holograms.modern-renderer.enabled`) with player heads on leaderboard rows (heads from 1.21.10) |

## Text

Default text comes from `config.yml`; per-parkour text from `/parkour sethologram <name> <type> <text>` with `|` as line separator.

```yaml
holograms:
  text:
    start:
      - "&e&lParkour Challenge"
      - "&a&lStart"
      - "&7Best: &e%best_time%"
    leaderboard:
      header:
        - "&e&lLeaderboard"
        - "&7Update every &e%update-interval%&7 %update-unit%"
      entry-format: "%pos% &8» %prefix%%player% &8- &e%time%"
      position-colors: { 1: "&6&l", 2: "&7&l", 3: "&c&l", default: "&e&l" }
      no-record-player: "Unknown"
      no-record-time: "--:--"
```

| Placeholder | Where | Meaning |
|---|---|---|
| `%parkour%` | header | Parkour name |
| `%update-interval%` `%update-unit%` | header | Refresh cadence, localized |
| `%pos%` | entry | Position with its colour, e.g. `&6&l#1` |
| `%prefix%` | entry | LuckPerms prefix when `show-prefix` is on |
| `%player%` `%time%` | entry | Name and formatted time |
| `%best_time%` | start hologram | Fastest recorded time |
| `%checkpoint%` | checkpoint hologram | Checkpoint number |
| `<head:%player%>` | entry (Pro) | Player head before the row (1.21.10+) |

## Period leaderboards (Pro)

```
/parkour addperiodleaderboard sky daily
/parkour addperiodleaderboard sky weekly
/parkour removeperiodleaderboard sky daily
```

They use `holograms.text.period-leaderboard.header` (with `%label%` and `%parkour%`) and the legacy entry format. Labels for `alltime`, `daily`, `weekly` and `monthly` are configurable. Old periods are pruned automatically.

## Positioning

`start-offset`, `end-offset`, `checkpoint-offset` and `leaderboard-offset` raise the hologram above its plate. `movehologram` moves one to the block you look at, `removehologram` hides one. `visibility-range` hides holograms beyond that distance.

## Refreshing

Leaderboards refresh every `update-interval` seconds and immediately after a new record, `deletetime`, `settime`, a season change and (Pro) a record from another server in the shared database.
