# Configuration

All settings live in `config.yml`. Run `/parkour reload` after editing. Keys marked **Pro** exist only in ParkourPro.

## General

| Key | Default | Description |
|---|---|---|
| `language` | `en_US` | One of the 23 bundled language codes. Files in `languages/` can be edited |
| `permissions.admin` | `parkour.admin` | Permission node for admin commands |
| `permissions.use-permissions` | `true` | `false` lets everyone use admin commands (not recommended) |
| `locks.enabled` | `true` | Global switch for required permission / required completion |
| `sounds.checkpoint` / `start` / `finish` / `reset` / `teleport-back` | vanilla sounds | Empty string disables. Per-parkour overrides with `/parkour setsound` |
| `checkpoints.sequential` | `true` | Checkpoints only count in order. `false` restores the old behaviour where a later checkpoint counts the earlier ones |

## MySQL

| Key | Default | Description |
|---|---|---|
| `mysql.enabled` | `false` | Store records, statistics and period records in MySQL |
| `mysql.host` / `port` / `database` / `username` / `password` | localhost:3306 | Connection details |
| `mysql.table-prefix` | `parkour_` | Only letters, digits and underscores |
| `mysql.sync-interval` **Pro** | `10` | Seconds between checks for records set on other servers sharing the database; changed parkours refresh their holograms immediately. `0` disables |

## Anti-cheat

| Key | Default | Description |
|---|---|---|
| `anti-cheat.detect-fly` | `true` | Flying players are reset to their checkpoint |
| `anti-cheat.detect-teleport` | `false` | Cancels teleports and player `/tp` during a run. Keep off when command blocks teleport players in your course |
| `anti-cheat.teleport-threshold` | `10.0` | Max distance per move when detect-teleport is on |
| `anti-cheat.detect-speed` **Pro** | `false` | Speed check: reset players moving faster than `max-horizontal-speed` blocks per movement packet for `speed-strikes` packets in a row. Speed potions raise the limit |

## Timer display

| Key | Default | Description |
|---|---|---|
| `timer-display.enabled` | `true` | Show the live timer |
| `timer-display.type` | `actionbar` | `actionbar`, `title`, `bossbar`, `disabled`; Pro adds `xpbar` |
| `timer-display.format` | | `%time%` and `%checkpoints%` |
| `timer-display.format-with-limit` **Pro** | | Adds `%timelimit%` and `%remaining%` |
| `timer-display.update-interval` | `10` | Ticks between updates |

## Fallback, death, leave

| Key | Default | Description |
|---|---|---|
| `fallback.y-enabled` / `default-y` | `false` / `65` | Global Y-level fallback |
| `fallback.blocks-enabled` / `default-blocks` **Pro** | `false` / `10` | Global fall-blocks rule |
| `fallback.teleport-target` | `reset` | `reset` or `checkpoint` |
| `death.global-enabled` | `true` | Handle deaths in every parkour |
| `death.respawn-to-checkpoint` | `true` | Respawn at the last checkpoint |
| `leave.teleport-to` | `reset` | `start`, `reset` or `none` |
| `bed-confirmation.enabled` / `double-click-time` | `true` / `1000` | Double-click the bed item to cancel |

## Holograms

| Key | Default | Description |
|---|---|---|
| `holograms.enabled` | `true` | Master switch |
| `holograms.update-interval` | `60` | Seconds between leaderboard refreshes (also refreshed instantly after records change) |
| `holograms.line-spacing` | `0.30` | Gap between lines |
| `holograms.start-offset` / `end-offset` / `checkpoint-offset` / `leaderboard-offset` | 0.5 / 0.5 / 0.5 / 2.0 | Height above the plate or block |
| `holograms.show-prefix` | `true` | LuckPerms prefix on leaderboard rows |
| `holograms.visibility-range` | `64` | Hide holograms beyond this distance, 0 = always visible |
| `holograms.modern-renderer.enabled` **Pro** | `false` | Packet-based HologramLib renderer on 1.20+ |
| `holograms.text.start` / `end` / `checkpoint` | lists | Default hologram lines; `%best_time%` and `%checkpoint%` |
| `holograms.text.leaderboard.header` / `entry-format` / `position-colors` / `no-record-*` | | See [Holograms](Holograms) |
| `holograms.text.period-leaderboard.header` / `labels` **Pro** | | Header lines and labels of the daily / weekly / monthly holograms |

## Items

| Key | Default | Description |
|---|---|---|
| `items.hotbar.teleport` / `reset` / `cancel` | plate / door / bed | `material`, `name`, `slot`, `click-type`, `lore` |
| `items.hotbar.inventory-mode` **Pro** | `full` | `full` clears the inventory, `slots` only clears `slots-to-clear` |

## Rewards and broadcast

| Key | Default | Description |
|---|---|---|
| `default-first-reward-commands` | empty | Commands every new parkour runs on a player's first completion |
| `default-timelimit` **Pro** | `0` | Seconds for new parkours |
| `default-penaltyoffline-commands` **Pro** | empty | Commands when a player disconnects mid-run |
| `broadcast.record.enabled` / `scope` | `false` / `server` | Announce new records to the `server` or `world` |
| `features.restart-on-same-start.enabled` | `false` | Stepping on your own start plate mid-run restarts the timer |
| `features.hide-players.*` **Pro** | all false | What `togglehideplayers` hides |
| `features.default-dynamic-hologram-visibility` **Pro** | `false` | Default for new parkours |
| `medals.*` **Pro** | off | Default thresholds (ms), per-course thresholds and reward commands |

## Update checker (both editions)

| Key | Default | Description |
|---|---|---|
| `update-checker.enabled` | `true` | Check the ParkourPro website for a newer release |
| `update-checker.notify-admins` | `true` | Tell players with `parkour.admin` on join |
| `update-checker.interval-hours` | `6` | Hours between checks |
| `update-checker.url` | wiki `version.json` | Where the latest version is published |

## Map boards (Pro)

```yaml
map-boards:
  default-width: 3
  default-height: 4
  header: "ParkourPro"        # your server name, top-left
  tag: "PARKOUR"              # pill top-right
  title: "Leaderboard: %parkour%"
  footer: "play.yourserver.net"
  show-heads: true
  colors:
    background: "#101215"
    header: "#F2B915"
    accent: "#FF5F9E"
    time: "#F2E15A"
    # ... panel, row, line, accent-text, title, name, rank, footer, gold, silver, bronze
```

## Discord webhook (both editions)

```yaml
discord-webhook:
  enabled: true
  url: "https://discord.com/api/webhooks/..."
  username: "ParkourPro"
  events:
    new-record: true
    first-completion: false
    season-end: true
  messages:
    new-record: ":trophy: **%player%** set a new record on **%parkour%**: **%time%**"
    first-completion: ":tada: **%player%** finished **%parkour%** for the first time in **%time%**"
    season-end: ":checkered_flag: Season **%season%** has ended! Records have been archived."
```

## Pro sections

```yaml
ghost:
  enabled: true
  auto-play-on-start: false     # start the ghost automatically when a run starts
  show-player-skin: true
  name-format: "&e%player% &7(Ghost &f%time%&7)"
  max-samples: 20000

race:
  min-players: 2
  max-players: 16
  countdown-seconds: 5
  timeout-seconds: 600
  countdown-sound: BLOCK_NOTE_BLOCK_PLING
  go-sound: ENTITY_PLAYER_LEVELUP
  winner-commands:
    - "eco give %player% 250"

seasons:
  broadcast: true
  reward-positions: 3
  rewards:
    1: ["eco give %player% 1000", "broadcast %player% won %parkour% this season!"]
    2: ["eco give %player% 500"]
    3: ["eco give %player% 250"]

web-api:
  enabled: false
  bind: 0.0.0.0
  port: 8567
  token: ""                     # Authorization: Bearer <token> or ?token=

worldguard:
  enabled: false
  regions: ["parkour_region"]

special-pressure-plates:
  enabled: true
  effects:
    jump: { amplifier: 2, duration-ticks: 80 }
    levitation: { amplifier: 1, duration-ticks: 40 }
  builders:
    remove-delay-ticks: 40
    replace-existing-blocks: true
    default-relative-blocks: ["0,-1,1", "0,-1,2", "0,-1,3"]

discord:                        # Discord bot, see the Discord page
  enabled: false
  token: ""
  guild-id: ""
  leaderboard-size: 10
```
