# FAQ and Troubleshooting

**The start plate does nothing.**
The parkour needs both a start and an end. Check that it is a gold plate. In Pro, check the WorldGuard region when that restriction is on. Locked parkours require the permission or prior completion, and cooldowns or daily limits may block the start (the player gets a message).

**Players get "you must complete all checkpoints".**
All checkpoints are required and must be activated in order. A player who skipped one sees "you skipped a checkpoint" on later plates. Pro can lower the number with `setrequiredcheckpoints`. Set `checkpoints.sequential: false` for the old behaviour.

**Command blocks teleport players and they get reset.**
Set `anti-cheat.detect-teleport: false`.

**Holograms are invisible or duplicated.**
`/parkour reload` removes and recreates every hologram. Check `holograms.visibility-range`. On modern Paper builds where the modern renderer causes issues keep `modern-renderer.enabled: false`.

**A cheater is on top of the leaderboard.**
`/parkour deletetime <parkour> <player>`. The hologram refreshes immediately.

**Records disappeared after switching between Pro and Lite.**
On first start the plugin copies `records.yml` from the other edition's folder when its own file has no records. With MySQL both share the same table.

**The time limit does not start.**
Set a leave position first: `/parkour setleaveposition <parkour>`.

**The ghost does not appear.**
A ghost exists only after someone set the fastest time since 1.0.9. `ghost.enabled` must be true. Use `/parkour ghost <parkour>`; the ghost is one shared armor stand per parkour.

**Speed check resets honest players.**
Raise `anti-cheat.max-horizontal-speed` or `speed-strikes`, or disable `detect-speed`. Ice and slime courses need higher values.

**Titles do not show on 1.8.**
Titles use NMS packets on 1.8. If a fork blocks them the text is sent to chat instead.

**Which Java do I need?**
Java 8 or newer.
