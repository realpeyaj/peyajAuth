# peyajAuth

A lightweight, secure, and modern authentication plugin for Minecraft servers (Paper 1.21+) and Velocity proxy networks.

![Java](https://img.shields.io/badge/Java-21-orange.svg)
![Platform](https://img.shields.io/badge/Platform-Paper%20%7C%20Velocity-blue.svg)
![Version](https://img.shields.io/badge/Version-1.7.1-green.svg)
[![bStats Paper](https://img.shields.io/bstats/servers/32544?color=blue&label=Paper)](https://bstats.org/plugin/bukkit/peyajAuth/32544)
[![bStats Velocity](https://img.shields.io/bstats/servers/34033?color=blue&label=Velocity)](https://bstats.org/plugin/velocity/peyajAuth/34033)

Are you a Filipino and want to host your Minecraft server in the Philippines? Visit https://mcziehost.fun

![web banner](https://i.imgur.com/D5vYv0R.jpeg)

> [!IMPORTANT]
> **Setup Requirement**: Set `online-mode=false` in `server.properties` (or `velocity.toml`). peyajAuth automatically validates official Mojang accounts while protecting offline/cracked players with passwords.

---

## Features

* **Auto-Login for Premium**: Official Minecraft accounts log in instantly with zero commands.
* **Password Protection**: Offline/cracked accounts register and log in with Argon2/BCrypt hashing.
* **Built-in Limbo Void**: Velocity proxies get an embedded virtual void world without needing an extra lobby server.
* **Bedrock & Geyser**: Seamless Floodgate support with Bedrock player auto-detection.
* **Account Safety**: 2FA (Google Authenticator), email recovery, anti-bot captchas, and brute-force lockouts.
* **Discord Alerts**: Real-time webhook notifications for registrations, logins, lockouts, and staff actions.
* **AuthMe Migration**: One-command database importer (`/auth import <file.db>`).

---

## Quick Setup

### Paper
1. Drop `peyajAuth-Paper-1.7.0.jar` into your `plugins/` folder.
2. Ensure `online-mode=false` in `server.properties`.
3. Restart your server.

### Velocity Proxy
1. Drop `peyajAuth-Velocity-1.7.0.jar` into your proxy `plugins/` folder.
2. Ensure `online-mode=false` in `velocity.toml`.
3. Restart Velocity.

---

## Commands

| Command | Description | Permission |
| :--- | :--- | :--- |
| `/register <password> <confirm>` | Register an account | Everyone |
| `/login <password>` | Log into your account | Everyone |
| `/changepassword <old> <new>` | Change account password | Everyone |
| `/2fa <setup\|confirm\|disable>` | Manage Google Authenticator | Everyone |
| `/email <add\|confirm>` | Manage recovery email | Everyone |
| `/auth reload` | Reload configuration files | OP / Admin |
| `/auth force <player>` | Force-authenticate a player | OP / Admin |
| `/auth unregister <player>` | Unregister a player account | OP / Admin |
| `/auth gui` | Open in-game admin menu | OP / Admin |

For developer API, configuration guide, and full documentation, visit the [Wiki](https://github.com/realpeyaj/peyajAuth/wiki).
