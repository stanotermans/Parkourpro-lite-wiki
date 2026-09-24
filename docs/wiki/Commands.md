# Commands

Root command: `/parkour` (aliases `/pk`, `/par`). `<angle brackets>` are required, `[square brackets]` are optional.
Admin commands need the `parkour.admin` permission (default: op). Player commands work for everyone with `parkour.use`.

Use the **Edition** column: Pro + Lite, Pro only or Lite only.

## Quick index

- [Course setup](#course-setup)
- [Rules & behaviour](#rules--behaviour)
- [Holograms](#holograms)
- [Records](#records)
- [Player commands](#player-commands)
- [Admin](#admin)

## Course setup

| Command | Edition | What it does |
|---|---|---|
| [`/parkour setstart <name>`](#setstart) | Pro + Lite | Sets the start plate. |
| [`/parkour setend <name>`](#setend) | Pro + Lite | Sets the finish plate. |
| [`/parkour addcheckpoint <name>`](#addcheckpoint) | Pro + Lite | Adds the **iron pressure plate** (heavy weighted) you look at as the next checkpoint. |
| [`/parkour setreset <name>`](#setreset) | Pro + Lite | Sets the reset location to where you stand. |
| [`/parkour setleaveposition <name>`](#setleaveposition) | Pro + Lite | Where players are teleported when they leave, cancel or run out of time. |
| [`/parkour wizard <name> <start\|cancel>`](#wizard) | Pro + Lite | Guided creation: start plate, end plate, checkpoints, then optional reset location, leave position and leaderboard. |
| [`/parkour create <name>`](#create) | **Pro only** | Creates an empty parkour you can fill in later with the other commands. |
| [`/parkour deletecheckpoint <parkour> <number>`](#deletecheckpoint) | **Pro only** | Removes checkpoint *number* (1-based) and renumbers the rest. |
| [`/parkour movecheckpoint <parkour> <number>`](#movecheckpoint) | **Pro only** | Moves an existing checkpoint to the iron plate you look at. |
| [`/parkour setrequiredcheckpoints <parkour> <number\|-1>`](#setrequiredcheckpoints) | **Pro only** | How many checkpoints (in order) a player must reach before the finish counts. |
| [`/parkour export <parkour>`](#export) | Pro + Lite | Writes the parkour to `plugins/<Plugin>/exports/<name>.yml` with all settings, holograms and coordinates relative to the start plate. |
| [`/parkour import <file> [newName]`](#import) | Pro + Lite | Look at the gold plate that becomes the new start, then import. |
| [`/parkour delete <name>`](#delete) | Pro + Lite | Deletes the parkour, its holograms, records and statistics. |

### setstart

```
/parkour setstart <name>
```

Edition: Pro + Lite

Sets the start plate. Look at a **gold pressure plate** (light weighted) while running the command. Creates the parkour if it does not exist.

Example:

```
/parkour setstart sky
```

> The plate you look at must be within 5 blocks.

### setend

```
/parkour setend <name>
```

Edition: Pro + Lite

Sets the finish plate. Look at a second **gold pressure plate**.

Example:

```
/parkour setend sky
```

### addcheckpoint

```
/parkour addcheckpoint <name>
```

Edition: Pro + Lite

Adds the **iron pressure plate** (heavy weighted) you look at as the next checkpoint. Run it once per plate, in course order.

Example:

```
/parkour addcheckpoint sky
```

> Checkpoints must be activated in order by players (see `checkpoints.sequential`).

### setreset

```
/parkour setreset <name>
```

Edition: Pro + Lite

Sets the reset location to where you stand. Used by `/parkour reset`, by falls without a checkpoint and, by default, when leaving.

Example:

```
/parkour setreset sky
```

### setleaveposition

```
/parkour setleaveposition <name>
```

Edition: Pro + Lite

Where players are teleported when they leave, cancel or run out of time. Falls back to the reset location when unset.

Example:

```
/parkour setleaveposition sky
```

> Required before a time limit can be set (Pro).

### wizard

```
/parkour wizard <name> <start|cancel>
```

Edition: Pro + Lite

Guided creation: start plate, end plate, checkpoints, then optional reset location, leave position and leaderboard. You get items to confirm, add a checkpoint, skip a step or cancel.

Example:

```
/parkour wizard sky start
```

> Your inventory is stored and restored when the wizard ends.

### create

```
/parkour create <name>
```

Edition: **Pro only**

Creates an empty parkour you can fill in later with the other commands.

Example:

```
/parkour create sky
```

### deletecheckpoint

```
/parkour deletecheckpoint <parkour> <number>
```

Edition: **Pro only**

Removes checkpoint *number* (1-based) and renumbers the rest.

Example:

```
/parkour deletecheckpoint sky 3
```

### movecheckpoint

```
/parkour movecheckpoint <parkour> <number>
```

Edition: **Pro only**

Moves an existing checkpoint to the iron plate you look at.

Example:

```
/parkour movecheckpoint sky 3
```

### setrequiredcheckpoints

```
/parkour setrequiredcheckpoints <parkour> <number|-1>
```

Edition: **Pro only**

How many checkpoints (in order) a player must reach before the finish counts. `-1` = all of them (default).

Example:

```
/parkour setrequiredcheckpoints sky 30
```

### export

```
/parkour export <parkour>
```

Edition: Pro + Lite

Writes the parkour to `plugins/<Plugin>/exports/<name>.yml` with all settings, holograms and coordinates relative to the start plate.

Example:

```
/parkour export sky
```

> New in 1.0.9.

### import

```
/parkour import <file> [newName]
```

Edition: Pro + Lite

Look at the gold plate that becomes the new start, then import. Every location is shifted relative to that plate, so a course can move to another world or server.

Example:

```
/parkour import sky sky_copy
```

> New in 1.0.9. Files are read from the `exports/` folder.

### delete

```
/parkour delete <name>
```

Edition: Pro + Lite

Deletes the parkour, its holograms, records and statistics. Players inside are removed from the run.

Example:

```
/parkour delete sky
```

> Cannot be undone. Export first if you might need it again.

## Rules & behaviour

| Command | Edition | What it does |
|---|---|---|
| [`/parkour togglefinishproximity <parkour> [radius]`](#togglefinishproximity) | **Pro only** | Finish when a player reaches the area of the end plate, without triggering the plate itself (jumping over it, sneaking). |
| [`/parkour togglefinishredirect <name>`](#togglefinishredirect) | **Pro only** | Teleport players back to the start plate after finishing. |
| [`/parkour toggleleaveredirect <name>`](#toggleleaveredirect) | Pro + Lite | Teleport to the start when leaving instead of the reset or leave position. |
| [`/parkour togglefallback <name>`](#togglefallback) | Pro + Lite | Enables the fallback rule configured with `setfallback` for this parkour. |
| [`/parkour setfallback y <name> <Y>`](#setfallback-lite) | **Lite only** | Teleport the player to the last checkpoint when they drop below this Y level. |
| [`/parkour setfallback <y\|blocks> <name> <value>`](#setfallback-pro) | **Pro only** | `y`: fall back below a Y level. |
| [`/parkour toggledeath <name>`](#toggledeath) | Pro + Lite | Treat dying like a fall: the player continues at their checkpoint. |
| [`/parkour toggledeathrespawn <name>`](#toggledeathrespawn) | Pro + Lite | Respawn inside the course after death instead of at the world spawn. |
| [`/parkour toggleitems <parkour> <true\|false>`](#toggleitems) | Pro + Lite | Whether players receive the hotbar items (teleport, reset, cancel) on this parkour. |
| [`/parkour togglelocks [true\|false]`](#togglelocks) | Pro + Lite | Global switch for locks (required permission / required completion). |
| [`/parkour setrequiredpermission <parkour> <permission\|none>`](#setrequiredpermission) | Pro + Lite | Only players with this permission can start the parkour. |
| [`/parkour setrequiredcompletion <parkour> <required-parkour\|none>`](#setrequiredcompletion) | Pro + Lite | Players must have finished another parkour first. |
| [`/parkour setleaveradius <parkour> <blocks\|0>`](#setleaveradius) | Pro + Lite | Cancels the run when the player is further than this many blocks from every plate (start, end, checkpoints). |
| [`/parkour setcooldown <parkour> <seconds\|0>`](#setcooldown) | Pro + Lite | Players must wait this long after finishing before starting the same parkour again. |
| [`/parkour setmaxattempts <parkour> <perDay\|0>`](#setmaxattempts) | Pro + Lite | Maximum number of starts per player per day (server local time). |
| [`/parkour setsound <parkour> <start\|checkpoint\|finish\|reset\|teleport-back> <SOUND\|none\|default>`](#setsound) | Pro + Lite | Per-parkour sound override. |
| [`/parkour settitle <parkour> <start\|finish> <title\|subtitle> <text\|none>`](#settitle) | Pro + Lite | Title shown when a run starts or finishes. |
| [`/parkour settimelimit <parkour> <seconds>`](#settimelimit) | **Pro only** | Players must finish within this time; `0` disables. |
| [`/parkour addpenalty <parkour> <command>`](#addpenalty) | **Pro only** | Console command run when the time limit expires. |
| [`/parkour addofflinepenalty <parkour> <command>`](#addofflinepenalty) | **Pro only** | Console command run when a player disconnects mid-run. |
| [`/parkour addendcommand <parkour> <command>`](#addendcommand) | Pro + Lite | Console command run on every finish. |
| [`/parkour addfirstreward <parkour> <command>`](#addfirstreward) | **Pro only** | Console command run once, on a player's very first completion. |
| [`/parkour setfirstreward <parkour> <command>`](#setfirstreward) | **Lite only** | Console command run once, on a player's first completion. |
| [`/parkour addtimereward <parkour> <mm:ss.ms> <command>`](#addtimereward) | **Pro only** | Console command for **every** finish under the time. |
| [`/parkour addtopreward <parkour> <position> <command>`](#addtopreward) | **Pro only** | Runs when a new personal best lands on that leaderboard position. |
| [`/parkour addrecordreward <parkour> <command>`](#addrecordreward) | **Pro only** | Runs on any new personal best. |
| [`/parkour rewards <parkour>`](#rewards) | **Pro only** | Lists every reward configured on the parkour (time, top, record and first-completion). |
| [`/parkour setcheckpointeffect <parkour> <checkpoint#> <title\|subtitle\|sound\|particle\|command\|clear> [value]`](#setcheckpointeffect) | **Pro only** | Title, sound, particle burst or console command when a checkpoint is reached. |
| [`/parkour togglehideplayers <parkour>`](#togglehideplayers) | **Pro only** | Hide other runners in the same parkour (body, tab list and/or chat, see `features.hide-players`). |
| [`/parkour testmode <parkour> <enabled\|disabled>`](#testmode) | **Pro only** | While enabled, first-completion, time, top and record rewards are not paid out. |
| [`/parkour togglemedals <parkour>`](#togglemedals) | **Pro only** | Starts a medal calibration run. |
| [`/parkour addeffectplate <parkour> <jump\|levitation>`](#addeffectplate) | **Pro only** | Turns the plate you look at into a special plate applying the effect. |
| [`/parkour addbuildplate <parkour> <block> [x,y,z ...]`](#addbuildplate) | **Pro only** | A plate that temporarily places blocks at the given offsets (default offsets from config), removed after a delay. |

### togglefinishproximity

```
/parkour togglefinishproximity <parkour> [radius]
```

Edition: **Pro only**

Finish when a player reaches the area of the end plate, without triggering the plate itself (jumping over it, sneaking). Radius 0.5–10 blocks, default 1. Passing a radius enables the option.

Example:

```
/parkour togglefinishproximity sky 1.5
```

> All finish rules (required checkpoints, records, rewards) still apply.

### togglefinishredirect

```
/parkour togglefinishredirect <name>
```

Edition: **Pro only**

Teleport players back to the start plate after finishing.

Example:

```
/parkour togglefinishredirect sky
```

### toggleleaveredirect

```
/parkour toggleleaveredirect <name>
```

Edition: Pro + Lite

Teleport to the start when leaving instead of the reset or leave position.

Example:

```
/parkour toggleleaveredirect sky
```

### togglefallback

```
/parkour togglefallback <name>
```

Edition: Pro + Lite

Enables the fallback rule configured with `setfallback` for this parkour.

Example:

```
/parkour togglefallback sky
```

### setfallback (Lite)

```
/parkour setfallback y <name> <Y>
```

Edition: **Lite only**

Teleport the player to the last checkpoint when they drop below this Y level.

Example:

```
/parkour setfallback y sky 60
```

### setfallback (Pro)

```
/parkour setfallback <y|blocks> <name> <value>
```

Edition: **Pro only**

`y`: fall back below a Y level. `blocks`: fall back after dropping this many blocks from the highest point since the last checkpoint (works at any height).

Example:

```
/parkour setfallback blocks sky 8
```

### toggledeath

```
/parkour toggledeath <name>
```

Edition: Pro + Lite

Treat dying like a fall: the player continues at their checkpoint.

Example:

```
/parkour toggledeath sky
```

### toggledeathrespawn

```
/parkour toggledeathrespawn <name>
```

Edition: Pro + Lite

Respawn inside the course after death instead of at the world spawn.

Example:

```
/parkour toggledeathrespawn sky
```

### toggleitems

```
/parkour toggleitems <parkour> <true|false>
```

Edition: Pro + Lite

Whether players receive the hotbar items (teleport, reset, cancel) on this parkour.

Example:

```
/parkour toggleitems sky false
```

### togglelocks

```
/parkour togglelocks [true|false]
```

Edition: Pro + Lite

Global switch for locks (required permission / required completion).

Example:

```
/parkour togglelocks true
```

### setrequiredpermission

```
/parkour setrequiredpermission <parkour> <permission|none>
```

Edition: Pro + Lite

Only players with this permission can start the parkour.

Example:

```
/parkour setrequiredpermission sky vip.parkour
```

### setrequiredcompletion

```
/parkour setrequiredcompletion <parkour> <required-parkour|none>
```

Edition: Pro + Lite

Players must have finished another parkour first.

Example:

```
/parkour setrequiredcompletion sky2 sky
```

### setleaveradius

```
/parkour setleaveradius <parkour> <blocks|0>
```

Edition: Pro + Lite

Cancels the run when the player is further than this many blocks from every plate (start, end, checkpoints). `0` disables.

Example:

```
/parkour setleaveradius sky 40
```

> New in 1.0.9.

### setcooldown

```
/parkour setcooldown <parkour> <seconds|0>
```

Edition: Pro + Lite

Players must wait this long after finishing before starting the same parkour again.

Example:

```
/parkour setcooldown sky 300
```

> New in 1.0.9.

### setmaxattempts

```
/parkour setmaxattempts <parkour> <perDay|0>
```

Edition: Pro + Lite

Maximum number of starts per player per day (server local time).

Example:

```
/parkour setmaxattempts sky 5
```

> New in 1.0.9.

### setsound

```
/parkour setsound <parkour> <start|checkpoint|finish|reset|teleport-back> <SOUND|none|default>
```

Edition: Pro + Lite

Per-parkour sound override. `none` mutes, `default` returns to config.yml. Tab completion lists every sound of your server version.

Example:

```
/parkour setsound sky finish ENTITY_ENDER_DRAGON_GROWL
```

> New in 1.0.9.

### settitle

```
/parkour settitle <parkour> <start|finish> <title|subtitle> <text|none>
```

Edition: Pro + Lite

Title shown when a run starts or finishes. Placeholders `%player%`, `%parkour%`, `%time%` (finish only). Colour codes with `&`.

Example:

```
/parkour settitle sky finish subtitle &aFinished in %time%!
```

> New in 1.0.9. Works on 1.8 as well.

### settimelimit

```
/parkour settimelimit <parkour> <seconds>
```

Edition: **Pro only**

Players must finish within this time; `0` disables. Requires a leave position.

Example:

```
/parkour settimelimit sky 120
```

### addpenalty

```
/parkour addpenalty <parkour> <command>
```

Edition: **Pro only**

Console command run when the time limit expires. `%player%` is replaced. Remove with `removepenalty <parkour> [command]`.

Example:

```
/parkour addpenalty sky eco take %player% 50
```

### addofflinepenalty

```
/parkour addofflinepenalty <parkour> <command>
```

Edition: **Pro only**

Console command run when a player disconnects mid-run. `setpenaltyoffline [parkour] <command>` sets the default, `removeofflinepenalty <parkour> [command]` removes.

Example:

```
/parkour addofflinepenalty sky eco take %player% 25
```

### addendcommand

```
/parkour addendcommand <parkour> <command>
```

Edition: Pro + Lite

Console command run on every finish. Remove with `removeendcommand <parkour>`.

Example:

```
/parkour addendcommand sky give %player% diamond 1
```

### addfirstreward

```
/parkour addfirstreward <parkour> <command>
```

Edition: **Pro only**

Console command run once, on a player's very first completion. Remove with `removefirstreward <parkour> [command]`.

Example:

```
/parkour addfirstreward sky eco give %player% 500
```

> Lite uses `setfirstreward <parkour> <command>` / `removefirstreward <parkour>`.

### setfirstreward

```
/parkour setfirstreward <parkour> <command>
```

Edition: **Lite only**

Console command run once, on a player's first completion. Remove with `removefirstreward <parkour>`.

Example:

```
/parkour setfirstreward sky eco give %player% 500
```

### addtimereward

```
/parkour addtimereward <parkour> <mm:ss.ms> <command>
```

Edition: **Pro only**

Console command for **every** finish under the time. Placeholders `%player%`, `%parkour%`, `%time%`. Remove with `removetimereward <parkour> <mm:ss.ms|all>`.

Example:

```
/parkour addtimereward sky 00:45.000 eco give %player% 100
```

> New in 1.0.9.

### addtopreward

```
/parkour addtopreward <parkour> <position> <command>
```

Edition: **Pro only**

Runs when a new personal best lands on that leaderboard position. `%pos%` available. Remove with `removetopreward <parkour> <position>`.

Example:

```
/parkour addtopreward sky 1 broadcast %player% is now #1 on %parkour%!
```

> New in 1.0.9.

### addrecordreward

```
/parkour addrecordreward <parkour> <command>
```

Edition: **Pro only**

Runs on any new personal best. `removerecordreward <parkour>` clears all.

Example:

```
/parkour addrecordreward sky give %player% emerald 1
```

> New in 1.0.9.

### rewards

```
/parkour rewards <parkour>
```

Edition: **Pro only**

Lists every reward configured on the parkour (time, top, record and first-completion).

Example:

```
/parkour rewards sky
```

> New in 1.0.9.

### setcheckpointeffect

```
/parkour setcheckpointeffect <parkour> <checkpoint#> <title|subtitle|sound|particle|command|clear> [value]
```

Edition: **Pro only**

Title, sound, particle burst or console command when a checkpoint is reached. `command` adds a command, `command none` clears them, `clear` removes everything. Placeholders `%player%`, `%checkpoint%`.

Example:

```
/parkour setcheckpointeffect sky 5 particle FLAME
```

> New in 1.0.9. Particles: HAPPY_VILLAGER, FLAME, HEART, CRIT, CLOUD, FIREWORKS_SPARK and any name of your version.

### togglehideplayers

```
/parkour togglehideplayers <parkour>
```

Edition: **Pro only**

Hide other runners in the same parkour (body, tab list and/or chat, see `features.hide-players`).

Example:

```
/parkour togglehideplayers sky
```

### testmode

```
/parkour testmode <parkour> <enabled|disabled>
```

Edition: **Pro only**

While enabled, first-completion, time, top and record rewards are not paid out.

Example:

```
/parkour testmode sky enabled
```

### togglemedals

```
/parkour togglemedals <parkour>
```

Edition: **Pro only**

Starts a medal calibration run. Finish the course, then `confirmmedals <parkour> <yes|no>` to save gold/silver/bronze thresholds.

Example:

```
/parkour togglemedals sky
```

### addeffectplate

```
/parkour addeffectplate <parkour> <jump|levitation>
```

Edition: **Pro only**

Turns the plate you look at into a special plate applying the effect. `removespecialplate <parkour>` removes it.

Example:

```
/parkour addeffectplate sky jump
```

### addbuildplate

```
/parkour addbuildplate <parkour> <block> [x,y,z ...]
```

Edition: **Pro only**

A plate that temporarily places blocks at the given offsets (default offsets from config), removed after a delay.

Example:

```
/parkour addbuildplate sky GLASS 0,-1,1 0,-1,2 0,-1,3
```

## Holograms

| Command | Edition | What it does |
|---|---|---|
| [`/parkour sethologram <name> <start\|end\|checkpoint\|leaderboard> <text>`](#sethologram) | Pro + Lite | Sets hologram text. |
| [`/parkour addleaderboard <name>`](#addleaderboard) | Pro + Lite | Creates (or moves) the leaderboard hologram at the block you look at. |
| [`/parkour setleaderboardsize <name> <size>`](#setleaderboardsize) | Pro + Lite | Number of entries on the leaderboard hologram. |
| [`/parkour movehologram <parkour> <start\|end\|leaderboard\|checkpoint[:#]>`](#movehologram) | Pro + Lite | Moves a hologram to the block you look at. |
| [`/parkour removehologram <parkour> <all\|start\|end\|leaderboard\|checkpoint[:#]>`](#removehologram) | Pro + Lite | Hides a hologram. |
| [`/parkour sethologramdisplay <parkour> <all\|start\|end\|checkpoint[:N]\|leaderboard> <background\|opacity\|seethrough\|billboard\|scale> <value>`](#sethologramdisplay) | **Pro only** | Styling for text-display holograms (Paper 1.19.4+): background hex or `transparent`, opacity 0–255, `seethrough true|false`, billboard `center|fixed|vertical|horizontal`, scale. |
| [`/parkour addperiodleaderboard <parkour> <daily\|weekly\|monthly>`](#addperiodleaderboard) | **Pro only** | Extra leaderboard hologram for the current day, ISO week or month at the block you look at. |
| [`/parkour mapboard <add <parkour> [alltime\|daily\|weekly\|monthly] [WxH] \| remove [parkour] \| list \| refresh>`](#mapboard) | **Pro only** | Leaderboard poster on maps in a grid of item frames: header, podium with player heads, ranked rows and footer. |
| [`/parkour toggledynamichologram <parkour>`](#toggledynamichologram) | **Pro only** | Each player only sees the hologram that matters for their progress. |

### sethologram

```
/parkour sethologram <name> <start|end|checkpoint|leaderboard> <text>
```

Edition: Pro + Lite

Sets hologram text. Separate lines with `|`. For a checkpoint: `sethologram <name> checkpoint <#> <text>`.

Example:

```
/parkour sethologram sky start &e&lSky Run|&7Beat 01:00 for a reward
```

### addleaderboard

```
/parkour addleaderboard <name>
```

Edition: Pro + Lite

Creates (or moves) the leaderboard hologram at the block you look at.

Example:

```
/parkour addleaderboard sky
```

### setleaderboardsize

```
/parkour setleaderboardsize <name> <size>
```

Edition: Pro + Lite

Number of entries on the leaderboard hologram.

Example:

```
/parkour setleaderboardsize sky 10
```

### movehologram

```
/parkour movehologram <parkour> <start|end|leaderboard|checkpoint[:#]>
```

Edition: Pro + Lite

Moves a hologram to the block you look at.

Example:

```
/parkour movehologram sky checkpoint:2
```

### removehologram

```
/parkour removehologram <parkour> <all|start|end|leaderboard|checkpoint[:#]>
```

Edition: Pro + Lite

Hides a hologram. Re-enable with `sethologram` or `addleaderboard`.

Example:

```
/parkour removehologram sky end
```

### sethologramdisplay

```
/parkour sethologramdisplay <parkour> <all|start|end|checkpoint[:N]|leaderboard> <background|opacity|seethrough|billboard|scale> <value>
```

Edition: **Pro only**

Styling for text-display holograms (Paper 1.19.4+): background hex or `transparent`, opacity 0–255, `seethrough true|false`, billboard `center|fixed|vertical|horizontal`, scale.

Example:

```
/parkour sethologramdisplay sky leaderboard scale 1.5
```

### addperiodleaderboard

```
/parkour addperiodleaderboard <parkour> <daily|weekly|monthly>
```

Edition: **Pro only**

Extra leaderboard hologram for the current day, ISO week or month at the block you look at. `removeperiodleaderboard <parkour> <period>` removes it.

Example:

```
/parkour addperiodleaderboard sky weekly
```

> New in 1.0.9.

### mapboard

```
/parkour mapboard <add <parkour> [alltime|daily|weekly|monthly] [WxH] | remove [parkour] | list | refresh>
```

Edition: **Pro only**

Leaderboard poster on maps in a grid of item frames: header, podium with player heads, ranked rows and footer. Hang the top-left item frame on a wall, look at it and run `add`. Missing frames of the grid are placed automatically. `remove` removes the board you look at (or all boards of a parkour), `refresh` re-renders everything.

Example:

```
/parkour mapboard add sky weekly 3x4
```

> New in 1.1.0. Default size 3x4 frames; colours, header, tag and footer under `map-boards` in config.yml.

### toggledynamichologram

```
/parkour toggledynamichologram <parkour>
```

Edition: **Pro only**

Each player only sees the hologram that matters for their progress.

Example:

```
/parkour toggledynamichologram sky
```

## Records

| Command | Edition | What it does |
|---|---|---|
| [`/parkour deletetime <parkour> <player>`](#deletetime) | Pro + Lite | Wipes a player's record, for example a cheater. |
| [`/parkour settime <parkour> <player> <mm:ss.ms>`](#settime) | Pro + Lite | Sets or overwrites a player's record, even when slower than their current one. |
| [`/parkour top <parkour> [daily\|weekly\|monthly] [page]`](#top) | Pro + Lite | Leaderboard in chat, ten per page, with your own rank at the bottom. |
| [`/parkour pb <parkour> [player]`](#pb) | Pro + Lite | Best time, rank, checkpoint splits of the best run, attempts, completions and play time. |
| [`/parkour stats <parkour> [player]`](#stats) | **Pro only** | Shows a player's best time and rank on a parkour. |
| [`/parkour leaderboard <parkour>`](#leaderboard) | **Pro only** | Prints the top list in chat. |
| [`/parkour season <info\|list\|new [name] confirm>`](#season) | **Pro only** | `info` shows the current season, `list` the closed ones. |

### deletetime

```
/parkour deletetime <parkour> <player>
```

Edition: Pro + Lite

Wipes a player's record, for example a cheater. Works for offline players and with MySQL. The leaderboard hologram refreshes instantly.

Example:

```
/parkour deletetime sky Notch
```

### settime

```
/parkour settime <parkour> <player> <mm:ss.ms>
```

Edition: Pro + Lite

Sets or overwrites a player's record, even when slower than their current one. Accepts `01:23.456`, `1:23.4`, `83.5`, `45`, `1:01:23.456`.

Example:

```
/parkour settime sky Notch 01:23.456
```

### top

```
/parkour top <parkour> [daily|weekly|monthly] [page]
```

Edition: Pro + Lite

Leaderboard in chat, ten per page, with your own rank at the bottom. Periods are Pro only.

Example:

```
/parkour top sky weekly 2
```

> New in 1.0.9. Player command (no admin permission needed).

### pb

```
/parkour pb <parkour> [player]
```

Edition: Pro + Lite

Best time, rank, checkpoint splits of the best run, attempts, completions and play time.

Example:

```
/parkour pb sky
```

> New in 1.0.9. Player command.

### stats

```
/parkour stats <parkour> [player]
```

Edition: **Pro only**

Shows a player's best time and rank on a parkour.

Example:

```
/parkour stats sky Notch
```

### leaderboard

```
/parkour leaderboard <parkour>
```

Edition: **Pro only**

Prints the top list in chat.

Example:

```
/parkour leaderboard sky
```

### season

```
/parkour season <info|list|new [name] confirm>
```

Edition: **Pro only**

`info` shows the current season, `list` the closed ones. `new` pays the rewards from `seasons.rewards` to the top players of every parkour, archives **all** records and starts fresh. The last argument must be `confirm`.

Example:

```
/parkour season new Winter 2026 confirm
```

> New in 1.0.9. Archived records go to records_archive.yml or `<prefix>records_archive`.

## Player commands

| Command | Edition | What it does |
|---|---|---|
| [`/parkour checkpoint`](#checkpoint) | Pro + Lite | Teleport to your last checkpoint. |
| [`/parkour undocheckpoint`](#undocheckpoint) | Pro + Lite | Go back one checkpoint. |
| [`/parkour reset`](#reset) | Pro + Lite | Restart the run from the reset location. |
| [`/parkour cancel`](#cancel) | Pro + Lite | Abort the run and leave the course. |
| [`/parkour leave`](#leave) | Pro + Lite | Leave the parkour. |
| [`/parkour join <parkour>`](#join) | **Pro only** | Teleport to the start of a parkour. |
| [`/parkour list`](#list) | **Pro only** | Lists all parkours. |
| [`/parkour menu [page]`](#menu) | **Pro only** | Opens an inventory with every parkour, your best time, rank and attempts. |
| [`/parkour ghost <parkour> [play\|loop\|stop\|delete]`](#ghost) | **Pro only** | Replays the fastest run as a ghost (armor stand with the record holder's head) in real time. |
| [`/parkour race <create <parkour>\|join <host>\|start\|leave\|cancel>`](#race) | **Pro only** | `create` opens a race lobby, others `join <host>`, the host runs `start`. |
| [`/parkour language <code>`](#language) | **Pro only** | Switches the server language, for example `nl_NL`. |

### checkpoint

```
/parkour checkpoint
```

Edition: Pro + Lite

Teleport to your last checkpoint.

Example:

```
/parkour checkpoint
```

### undocheckpoint

```
/parkour undocheckpoint
```

Edition: Pro + Lite

Go back one checkpoint.

Example:

```
/parkour undocheckpoint
```

### reset

```
/parkour reset
```

Edition: Pro + Lite

Restart the run from the reset location. The timer restarts.

Example:

```
/parkour reset
```

### cancel

```
/parkour cancel
```

Edition: Pro + Lite

Abort the run and leave the course.

Example:

```
/parkour cancel
```

### leave

```
/parkour leave
```

Edition: Pro + Lite

Leave the parkour. Pro also registers a plain `/leave`.

Example:

```
/parkour leave
```

### join

```
/parkour join <parkour>
```

Edition: **Pro only**

Teleport to the start of a parkour.

Example:

```
/parkour join sky
```

### list

```
/parkour list
```

Edition: **Pro only**

Lists all parkours.

Example:

```
/parkour list
```

### menu

```
/parkour menu [page]
```

Edition: **Pro only**

Opens an inventory with every parkour, your best time, rank and attempts. Click an entry to teleport to its start.

Example:

```
/parkour menu
```

> New in 1.0.9. Permission `parkour.menu` (default true).

### ghost

```
/parkour ghost <parkour> [play|loop|stop|delete]
```

Edition: **Pro only**

Replays the fastest run as a ghost (armor stand with the record holder's head) in real time. `loop` repeats it, `stop` removes it, `delete` (admin) erases the recording. The fastest run is recorded automatically.

Example:

```
/parkour ghost sky loop
```

> New in 1.0.9. Permission `parkour.ghost` (default true). One ghost per parkour, visible to everyone.

### race

```
/parkour race <create <parkour>|join <host>|start|leave|cancel>
```

Edition: **Pro only**

`create` opens a race lobby, others `join <host>`, the host runs `start`. A countdown freezes everyone on the start plate, all runs begin on GO, the first over the finish wins.

Example:

```
/parkour race create sky
```

> New in 1.0.9. Permission `parkour.race` (default true). Settings under `race` in config.yml.

### language

```
/parkour language <code>
```

Edition: **Pro only**

Switches the server language, for example `nl_NL`.

Example:

```
/parkour language nl_NL
```

## Admin

| Command | Edition | What it does |
|---|---|---|
| [`/parkour version`](#version) | Pro + Lite | Shows the installed version and checks the ParkourPro website for a newer release. |
| [`/parkour reload`](#reload) | Pro + Lite | Reloads config, parkours, holograms, timer display and languages. |

### version

```
/parkour version
```

Edition: Pro + Lite

Shows the installed version and checks the ParkourPro website for a newer release.

Example:

```
/parkour version
```

> New in 1.1.0. Admins are also told on join when an update is available (`update-checker` in config.yml).

### reload

```
/parkour reload
```

Edition: Pro + Lite

Reloads config, parkours, holograms, timer display and languages. Pro also re-registers Discord commands and restarts the web API and network sync.

Example:

```
/parkour reload
```
