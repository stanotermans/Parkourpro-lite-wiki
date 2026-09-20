# Placeholders

## PlaceholderAPI

With PlaceholderAPI installed the `parkour` expansion registers automatically. Use `auto` as the parkour name when you only have one parkour.

| Placeholder | Result |
|---|---|
| `%parkour_top_<parkour>_<1-10>_player%` | Player name at that position, `---` when empty |
| `%parkour_top_<parkour>_<1-10>_time%` | Time at that position, `--:--` when empty |
| `%parkour_top_<parkour>_<1-10>_prefix%` | LuckPerms prefix of that player |
| `%parkour_personal_<parkour>_time%` | The viewer's best time |
| `%parkour_personal_<parkour>_rank%` | The viewer's rank |
| `%parkour_current%` | Parkour the viewer is running, empty when none |
| `%parkour_current_time%` | Live elapsed time |
| `%parkour_current_checkpoint%` | Current checkpoint number |
| `%parkour_current_checkpoints%` | Number of checkpoints of the current parkour |
| `%parkour_attempts_<parkour>%` | The viewer's attempts |
| `%parkour_completions_<parkour>%` | The viewer's completions |
| `%parkour_playtime_<parkour>%` | The viewer's play time, e.g. `1h 12m 5s` |
| `%parkour_racewins_<parkour>%` | The viewer's race wins (Pro) |
| `%parkour_count%` | Number of parkours |

Example scoreboard lines:

```yaml
- "&6#1 &f%parkour_top_sky_1_player% &7- &e%parkour_top_sky_1_time%"
- "&bYou: &f%parkour_personal_sky_time% &7(#%parkour_personal_sky_rank%)"
- "&7Now: &e%parkour_current% &f%parkour_current_time%"
```

Values are cached for five seconds.

## Message placeholders

Inside language files, hologram text, titles and reward commands:

| Placeholder | Meaning |
|---|---|
| `%player%` | Player name |
| `%parkour%` | Parkour name |
| `%time%` | Formatted time |
| `%time_ms%` | Time in milliseconds (reward commands) |
| `%pos%` / `%rank%` | Leaderboard position (rewards, races) |
| `%checkpoint%` | Checkpoint number |
| `%completed%` / `%total%` | Checkpoint progress |
| `%record%` | Existing record |
| `%diff%` | Split difference, pre-coloured |
| `%seconds%` | Cooldown or countdown seconds |
| `%season%` / `%new-season%` | Season names |

Colour codes use `&`, hex colours `#RRGGBB`. An empty message string disables that message.
