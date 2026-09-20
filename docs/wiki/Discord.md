# Discord

## Webhook (Pro and Lite)

No bot needed. In your Discord channel settings create a webhook and paste its URL:

```yaml
discord-webhook:
  enabled: true
  url: "https://discord.com/api/webhooks/..."
  events:
    new-record: true
    first-completion: false
    season-end: true
```

Messages are templates with `%player%`, `%parkour%`, `%time%` and `%season%`. Colour codes are stripped; Discord markdown and emoji shortcodes work.

## Bot (Pro)

The built-in bot answers `/scoreboard parkour:<name>` with a rich embed of the top times.

1. In the Discord Developer Portal create an application, add a bot and copy its token. Invite it with the `applications.commands` scope.
2. Set `discord.enabled: true`, paste the `token` and optionally a `guild-id` for instant command registration.
3. Style the embed: `title`, `color`, `entry-format` (`%pos%`, `%player%`, `%time%`, `%rank%`), `footer`, `empty-message`, column labels and `leaderboard-size`. With LuckPerms and `show-prefix` the rank prefix is included.
4. `/parkour reload` re-registers the slash command.

Player heads can be shown inline as guild emojis (`inline-head-emojis`); head URLs are cached for `avatar-cache-minutes`.
