# Installation

## Requirements

| Component | Supported |
|---|---|
| Server | Spigot, Paper and forks (Purpur, Pufferfish, ...) |
| Minecraft | 1.8 through 26.x |
| Java | 8 or newer (the jar is Java 8 bytecode) |
| Optional | LuckPerms (prefixes), PlaceholderAPI (placeholders), ItemsAdder; Pro: WorldGuard, WorldEdit, ProtocolLib, DecentHolograms |

## First start

1. Put `ParkourPro-1.1.0.jar` **or** `ParkourProLite-1.1.0.jar` in `plugins/`. Never run both at once.
2. Restart the server. The plugin creates `config.yml`, `parkours.yml`, `records.yml`, `stats.yml` and a `languages/` folder with 23 translations.
3. Set `language` in `config.yml` (for example `nl_NL`).
4. Optional: enable `mysql` for networks. Without MySQL everything is stored in YAML files.
5. Apply changes with `/parkour reload`.

## Upgrading

Replace the old jar with the new one and restart. Configurations, parkours and records stay compatible. New config keys and messages are added automatically; existing language files receive missing keys in English.

With MySQL the new tables (`<prefix>stats`, `<prefix>period_records`) and the `splits` column are created on the first connect.

## Switching between Pro and Lite

Both editions keep their own folder (`plugins/ParkourPro` and `plugins/ParkourProLite`). On the first start, the plugin copies `records.yml` from the other edition's folder when its own file has no records. With MySQL both editions share the same tables.

## Files

| File | Contents |
|---|---|
| `config.yml` | All settings, see [Configuration](Configuration) |
| `parkours.yml` | Every parkour: plates, checkpoints, holograms, toggles, rewards |
| `records.yml` | Best time per player per parkour, with checkpoint splits |
| `stats.yml` | Attempts, completions, play time, race wins |
| `languages/*.yml` | Messages per language |
| `exports/` | Files written by `/parkour export` |
| Pro: `period_records.yml`, `seasons.yml`, `records_archive.yml`, `ghosts/` | Period leaderboards, seasons, archived records, ghost recordings |
