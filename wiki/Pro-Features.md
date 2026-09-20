# Pro Features

## Proximity finish

`/parkour togglefinishproximity <parkour> [radius]` ends the run as soon as a player is within the radius of the end plate, even if the plate is never pressed. Required checkpoints, records, rewards and redirects behave exactly as with the plate.

## Ghost replay

Every run is sampled about twenty times per second. When a run becomes the fastest time on a parkour it is saved to `ghosts/<parkour>.yml`.

```
/parkour ghost sky            # play once
/parkour ghost sky loop       # repeat
/parkour ghost sky stop
/parkour ghost sky delete     # admin
```

The ghost is an armor stand with the record holder's head that follows the recorded path in real time. `ghost.auto-play-on-start: true` starts it automatically when someone starts the parkour. Permission `parkour.ghost`.

## Race mode

```
/parkour race create sky      # host opens a lobby
/parkour race join Stan       # others join the host
/parkour race start           # host starts the countdown
/parkour race leave
/parkour race cancel          # host
```

Everyone is teleported to the start plate and frozen during the countdown (titles and sounds). All runs start on GO. Positions are announced to the racers, the winner gets `race.winner-commands` and a race win in the statistics. Leaving a started race counts as a forfeit. Permission `parkour.race`.

## Daily, weekly and monthly leaderboards

Every finish updates the player's best for the current day, ISO week and month.

- Chat: `/parkour top sky daily|weekly|monthly`
- Holograms: `/parkour addperiodleaderboard sky weekly`
- API: `/api/leaderboard/sky?period=weekly`

Old periods are pruned automatically. Stored in `period_records.yml` and `<prefix>period_records`.

## Seasons

`/parkour season new Winter confirm` closes the season: rewards from `seasons.rewards` go to the top players of every parkour, all records are archived and the leaderboards start empty. The change is broadcast and posted to the Discord webhook.

## Menu

`/parkour menu` opens an inventory with every parkour, your best time and rank, the record holder and your attempts. Click to teleport to the start. Permission `parkour.menu`.

## Rewards

| Command | Fires |
|---|---|
| `addtimereward <parkour> <mm:ss.ms> <command>` | Every finish under the time |
| `addtopreward <parkour> <position> <command>` | A new personal best that lands on that position |
| `addrecordreward <parkour> <command>` | Any new personal best |
| `addfirstreward <parkour> <command>` | The very first completion |
| `rewards <parkour>` | Lists all of the above |

Placeholders `%player%`, `%parkour%`, `%time%`, `%time_ms%`, `%pos%`. Testing mode (`testmode`) suppresses all of them.

## Checkpoint effects

`/parkour setcheckpointeffect sky 5 title &aHalfway!`, `... sound ENTITY_PLAYER_LEVELUP`, `... particle FLAME`, `... command give %player% cookie 1`, `... clear`.

## Speed check

`anti-cheat.detect-speed: true` resets players that move faster than `max-horizontal-speed` blocks per movement packet for `speed-strikes` packets in a row. Speed potions raise the limit. Off by default; tune it per server.

## Time limits and penalties

`settimelimit` puts a countdown in the timer. When it expires the player is sent to the leave position and penalty commands run. Offline-penalty commands run when a player disconnects mid-run.

## Special pressure plates

Effect plates give a jump boost or levitation, build plates place temporary blocks at configurable offsets.

## Medals

`togglemedals`, complete the course as the calibration run, `confirmmedals <parkour> yes`. Gold, silver and bronze thresholds are derived from the run; reward commands per medal fire when a player earns or improves a medal.

## Network sync

With a shared MySQL database, `mysql.sync-interval` polls for records set on other servers and refreshes the affected holograms right away.

## Web API

Enable `web-api.enabled`. Read-only JSON:

```
GET /api/parkours
GET /api/leaderboard/<parkour>?limit=10&period=alltime|daily|weekly|monthly
GET /api/player/<name>
GET /api/stats/<parkour>
GET /api/season
```

With `web-api.token` set, send `Authorization: Bearer <token>` or `?token=`. Responses include `Access-Control-Allow-Origin: *`.

## Hide players, dynamic holograms, testing mode, WorldGuard, ItemsAdder

`togglehideplayers` hides other runners' bodies, tab entries or chat inside the same parkour. `toggledynamichologram` shows each player only the hologram for their next target. `testmode` disables rewards while you build. `worldguard.regions` restricts plates to regions. With ItemsAdder the timer shows custom icons.
