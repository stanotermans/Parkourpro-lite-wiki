# Getting Started

A course consists of three kinds of pressure plates:

| Plate | Block | Role |
|---|---|---|
| Start | Gold (light weighted pressure plate) | Stepping on it starts the run and the timer |
| End | Gold (light weighted pressure plate) | Finishes the run and saves the time |
| Checkpoint | Iron (heavy weighted pressure plate) | Players teleport back to the last one reached; must be activated in order |

## Six commands

Look at the plate while running each command (within 5 blocks).

```
/parkour setstart sky          # look at the gold start plate
/parkour setend sky            # look at the gold finish plate
/parkour addcheckpoint sky     # look at each iron plate, in course order
/parkour setreset sky          # stand where players restart after /parkour reset
/parkour addleaderboard sky    # look at the block where the top list should float
/parkour setleaderboardsize sky 10
```

Protect the course against falls:

```
/parkour setfallback y sky 60
/parkour togglefallback sky
```

## With the wizard

```
/parkour wizard sky start
```

| Step | What to do | Item |
|---|---|---|
| 1 Start | Stand on a gold plate, right-click **Confirm** | Stone |
| 2 End | Stand on another gold plate, right-click **Confirm** | Stone |
| 3 Checkpoints | Stand on each iron plate, right-click **Add Checkpoint**; right-click **Checkpoints Done** when finished | Iron ingot / Gold ore |
| 4 Reset location | Stand where players reset to, **Confirm** or **Skip** | Stone / Feather |
| 5 Leave position | Stand where players go when leaving, **Confirm** or **Skip** | Stone / Feather |
| 6 Leaderboard | Look at a block, **Confirm** or **Skip** | Stone / Feather |
| Any | Cancel and discard | Coal ore |

`/parkour wizard sky cancel` discards everything.

## Test it

Walk onto the start plate. You get three hotbar items: a plate (teleport to last checkpoint), a door (reset) and a bed (double-click to cancel). The timer appears in the action bar. Step on every checkpoint in order and finish on the end plate.

Useful next steps:

- `/parkour sethologram sky start &e&lSky Run|&7Beat 01:00!`
- `/parkour addendcommand sky give %player% diamond 1`
- `/parkour settitle sky finish title &a&lFinished!`
- Pro: `/parkour togglefinishproximity sky`, `/parkour settimelimit sky 120`, `/parkour addtimereward sky 00:45.000 eco give %player% 100`
