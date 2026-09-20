# Records and Statistics

## Records

A record is one best time per player per parkour. Only faster runs replace it, unless an admin overrides it with `settime`.

| Storage | Location |
|---|---|
| Local | `records.yml` (always written, even with MySQL on) |
| MySQL | table `<prefix>records`, one row per player and parkour, with a `splits` column |

Leaderboards read MySQL first and fall back to the local file.

## Checkpoint splits

Every checkpoint shows the elapsed time and the difference with your own record:

```
Checkpoint 3: 00:41.250 (+0.420)
Checkpoint 4: 00:58.100 (-1.100)
```

Green means you are ahead of your record, red means behind. Splits are stored together with the record and shown by `/parkour pb`.

## Statistics

Per player and parkour: attempts, completions, play time and race wins. Stored in `stats.yml` and, with MySQL, in `<prefix>stats`. Shown by `/parkour pb`, the Pro menu, [placeholders](Placeholders) and the Pro web API. Statistics also drive cooldowns (`setcooldown`) and daily limits (`setmaxattempts`).

## Managing records

```
/parkour deletetime sky Notch            # wipe Notch's record (cheater)
/parkour settime sky Notch 01:23.456     # set Notch's record
/parkour top sky                         # leaderboard in chat
/parkour top sky weekly                  # Pro: this week's leaderboard
/parkour pb sky Notch                    # Notch's best, rank, splits, stats
```

Player lookup works for offline players: online player first, then stored records on that parkour, then on any parkour, then the server's player data. The leaderboard hologram is redrawn immediately.

## Time format

| Input | Meaning |
|---|---|
| `01:23.456` | 1 minute, 23 seconds, 456 ms |
| `1:23.4` | fraction may have 1–3 digits |
| `83.5` or `45` | seconds only |
| `1:01:23.456` | hours, minutes, seconds |
| `01:23,456` | comma decimal is accepted |
| `1:60.000`, `abc`, `0` | rejected |

## Seasons (Pro)

`/parkour season new <name> confirm` pays `seasons.rewards` to the top `reward-positions` players of every parkour, moves every record to `records_archive.yml` (and `<prefix>records_archive`) and starts with empty leaderboards. `/parkour season info` and `list` show the state and history. Period leaderboards and statistics are kept.
