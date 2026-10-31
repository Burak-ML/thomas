# Thomas Bot

[![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
![Node.js](https://img.shields.io/badge/Node.js-18%2B-43853D?logo=node.js&logoColor=white)
![discord.js](https://img.shields.io/badge/discord.js-v14-5865F2?logo=discord&logoColor=white)

**A Discord bot that registers new members: they pick their field, the bot assigns the right roles and logs it.**

When someone joins the server, Thomas gives them a temporary "unregistered" role and points them to a registration panel. They choose their professions from a menu and confirm with a button. The bot then swaps the temporary role for the member role, adds the chosen profession roles and writes the result to a log channel.

## How it works

1. **Join.** A new member automatically receives the `Junior 1` and `Unregistered` roles, and a welcome message points them to the registration channel.
2. **Register.** In the registration panel the member selects one or more professions and presses the confirm button.
3. **Done.** The bot removes `Unregistered`, adds `Member` and the selected profession roles, posts a log entry and shows the member a private confirmation.

Available professions: Web Designer, Game Designer, Backend Developer, Frontend Developer, Mobile Developer, UI/UX Designer, Content Creator and Other.

## Commands

| Command | Who | Purpose |
|---------|-----|---------|
| `/setup-kayit [kanal]` | Admin | Post the registration panel in a channel (default: the current one) |
| `/kayitsizlar` | Admin | List members who have not registered yet |

## Getting started

Requires Node.js 18 or later and a Discord application with a bot token.

```bash
git clone https://github.com/Burak-ML/thomas.git
cd thomas
npm install
cp .env.example .env
```

Fill in `.env`. All IDs are Discord snowflakes (enable Developer Mode in Discord, then right-click an item and choose Copy ID).

```env
DISCORD_TOKEN=your_bot_token
CLIENT_ID=your_application_id
GUILD_ID=your_server_id

# Channels
KAYIT_KANAL_ID=registration channel
LOG_KANAL_ID=log channel
GIRIS_KANAL_ID=welcome channel (optional)

# Roles
KAYITSIZ_ROL_ID=unregistered role
JUNIOR1_ROL_ID=role given on join
UYE_ROL_ID=member role given after registration

# Profession roles
ROL_WEB_DESIGNER=...
ROL_GAME_DESIGNER=...
ROL_BACKEND_DEV=...
ROL_FRONTEND_DEV=...
ROL_MOBILE_DEV=...
ROL_UIUX_DESIGNER=...
ROL_CONTENT_CREATOR=...
ROL_OTHER=...
```

Register the slash commands once, then start the bot:

```bash
npm run deploy
npm start          # or: npm run dev   (restarts on file changes)
```

Finally, run `/setup-kayit` in the registration channel to post the panel. The bot's role must sit above the roles it assigns.

## Deployment

The repository includes a `Procfile` and `railway.toml`, so it runs on [Railway](https://railway.app) without extra setup. Connect the repository and add the same environment variables.

## Project structure

```
src/
  index.js            client setup and event loading
  config.js           IDs and role mapping read from the environment
  commands/           /setup-kayit and /kayitsizlar
  events/             ready, guildMemberAdd, interactionCreate
  utils/              embeds and the registration logic
deploy-commands.js    registers the slash commands with Discord
```

## License

MIT. See [LICENSE](LICENSE).
