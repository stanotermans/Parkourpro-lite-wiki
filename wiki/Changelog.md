# Changelog

## 1.0.9

### Pro and Lite

- **Checkpoint splits**: every checkpoint shows your elapsed time and the difference with your own record (`+0.420` red / `-1.100` green). Splits are stored with the record (`records.yml` and MySQL column `splits`) and shown by `/parkour pb`.
- **Player commands**: `/parkour top <parkour> [page]` prints the leaderboard in chat, `/parkour pb <parkour> [player]` shows best time, rank, splits and statistics.
- **Statistics**: attempts, completions, play time and race wins per player and parkour (`stats.yml`, MySQL table `<prefix>stats`).
- **Placeholders**: `%parkour_current%`, `%parkour_current_time%`, `%parkour_current_checkpoint%`, `%parkour_current_checkpoints%`, `%parkour_top_<parkour>_<pos>_prefix%`, `%parkour_attempts_<parkour>%`, `%parkour_completions_<parkour>%`, `%parkour_playtime_<parkour>%`, `%parkour_racewins_<parkour>%`.
- **Leave radius**: `/parkour setleaveradius <parkour> <blocks|0>` cancels the run when a player wanders too far from every plate of the course.
- **Cooldown and daily limit**: `/parkour setcooldown <parkour> <seconds|0>` and `/parkour setmaxattempts <parkour> <perDay|0>`.
- **Per-parkour sounds and titles**: `/parkour setsound <parkour> <type> <SOUND|none|default>` and `/parkour settitle <parkour> <start|finish> <title|subtitle> <text|none>`. Titles work on 1.8 through modern versions.
- **Export / import**: `/parkour export <parkour>` writes `exports/<name>.yml`; `/parkour import <file> [newName]` rebuilds the parkour relative to the gold plate you look at, in any world.
- **Creation wizard** now has three optional extra steps: reset location, leave position and leaderboard block (confirm or skip).
- **Discord webhook** (no bot needed): `discord-webhook` in config.yml posts new records, first completions and season changes.

### Pro only

- **Ghost replay**: the fastest run of every parkour is recorded automatically. `/parkour ghost <parkour> [play|loop|stop|delete]` replays it as an armor stand with the record holder's head. Optional auto-play when a run starts.
- **Race mode**: `/parkour race create <parkour>`, `join <host>`, `start`, `leave`, `cancel`. Countdown with titles, players frozen on the start plate, first over the finish wins, race wins are tracked.
- **Daily / weekly / monthly leaderboards**: `/parkour top <parkour> daily|weekly|monthly`, holograms with `/parkour addperiodleaderboard <parkour> <period>`, placeholders through the API. Old periods are pruned automatically.
- **Seasons**: `/parkour season new [name] confirm` pays the configured rewards to the top players of every parkour, archives all records and starts fresh. `season info` / `season list`.
- **Menu**: `/parkour menu` opens an inventory with every parkour, your best time, rank and attempts; click to teleport to the start.
- **Speed check**: `anti-cheat.detect-speed` with `max-horizontal-speed` and `speed-strikes` (off by default).
- **Rewards by time and rank**: `addtimereward`, `addtopreward`, `addrecordreward` (and remove variants), `/parkour rewards <parkour>` lists everything.
- **Network sync**: `mysql.sync-interval` refreshes leaderboard holograms when another server sharing the database sets a record.
- **Checkpoint effects**: `/parkour setcheckpointeffect <parkour> <#> <title|subtitle|sound|particle|command|clear> [value]`.
- **Web API**: read-only JSON on `web-api.port` (`/api/parkours`, `/api/leaderboard/<parkour>`, `/api/player/<name>`, `/api/stats/<parkour>`, `/api/season`), optional bearer token.

### Other

- New permissions with default true: `parkour.race`, `parkour.ghost`, `parkour.menu`.
- New messages in the English defaults and the en_US / nl_NL files; other languages receive English automatically.
- Everything is compiled to Java 8 bytecode and uses only API available from Minecraft 1.8 onwards, with version fallbacks for titles, particles and skulls.

## 1.0.8

### New commands (Pro and Lite)

- `/parkour deletetime <parkour> <player>` – wipes a player's record (for example a cheater). Works for offline players and with MySQL. The leaderboard hologram refreshes instantly.
- `/parkour settime <parkour> <player> <mm:ss.ms>` – sets or overwrites a player's record. Accepts `01:23.456`, `1:23.4`, `83.5`, `45` and `1:01:23.456`. The leaderboard hologram refreshes instantly.
- Tab completion for both commands: parkour names, player names (online players plus players with a stored record) and an example time format.

### New in Pro

- `/parkour togglefinishproximity <parkour> [radius]` – lets players finish by reaching the end plate area, without having to trigger the gold pressure plate (jumping over it, sneaking, etc.). Optional radius from 0.5 to 10 blocks, default 1.0. All finish rules (required checkpoints, records, rewards, end commands, redirect) still apply.

### Checkpoints (Pro and Lite)

- Checkpoints must now be activated in order. Stepping on a later checkpoint while an earlier one was skipped no longer counts and shows a "you skipped a checkpoint" message. Configurable with `checkpoints.sequential` (default `true`).

### Other

- New messages added to the built-in defaults and to the en_US and nl_NL language files. Other languages receive the English text automatically.
- Version bumped to 1.0.8.
- Compatible with Minecraft 1.8 through 26.x, like the rest of the plugin.

## 1.0.7-1

- Both editions run on Minecraft 26.2.
- Fixed the TPS and lag issue caused by the leaderboard hologram.
- Fixed the reset look position.
- Pro: a parkour only needs a start and an end; checkpoints are optional.
