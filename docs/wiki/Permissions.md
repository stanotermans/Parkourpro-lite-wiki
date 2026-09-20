# Permissions

| Node | Default | Grants |
|---|---|---|
| `parkour.admin` | op | All setup, rules, hologram, record, reward and reload commands. Rename with `permissions.admin` |
| `parkour.use` | everyone | Running parkours and the player commands (`checkpoint`, `reset`, `cancel`, `leave`, `top`, `pb`) |
| `parkour.race` (Pro) | everyone | Creating and joining races |
| `parkour.ghost` (Pro) | everyone | Playing ghost replays (`delete` still needs `parkour.admin`) |
| `parkour.menu` (Pro) | everyone | Opening the parkour menu |
| custom | – | Any node set with `setrequiredpermission` is checked before a run starts |

`permissions.use-permissions: false` disables the admin check entirely.
