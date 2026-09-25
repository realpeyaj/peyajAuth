# peyajAuth

A simple, fast, and secure login plugin for Minecraft servers (Paper 1.21.X - 26.X) and Velocity networks.

![Java](https://img.shields.io/badge/Java-21-orange.svg)
![Platform](https://img.shields.io/badge/Platform-Paper%20%7C%20Velocity-blue.svg)
![Version](https://img.shields.io/badge/Version-1.6.9-green.svg)
![License](https://img.shields.io/badge/License-Proprietary-red.svg)
[![bStats Paper](https://img.shields.io/bstats/servers/32544?color=blue&label=Paper%20Servers)](https://bstats.org/plugin/bukkit/peyajAuth/32544)
[![bStats Velocity](https://img.shields.io/bstats/servers/34033?color=blue&label=Velocity%20Servers)](https://bstats.org/plugin/velocity/peyajAuth/34033)

Are you a Filipino and want to host your Minecraft server in the Philippines? Visit https://mcziehost.fun

![web banner](https://i.imgur.com/D5vYv0R.jpeg)

> [!IMPORTANT]
> **Server Setup Tip**: Make sure your server (or Velocity proxy) is set to `online-mode=false`. The plugin will automatically check paid accounts and log them in safely, while letting non-paid players register with a password.

---

## What is peyajAuth?

peyajAuth makes managing player logins easy and stress-free. Players who purchased the official game can hop in without typing anything, while players without an official account are safely asked to create a password.

---

## Key Features

*   **Automatic Login for Paid Accounts**: Official Minecraft players join instantly without needing to remember or type a password.
*   **Password Protection for Free Accounts**: Players who use offline or cracked launchers can safely protect their account with `/register` and `/login`.
*   **Built-in Waiting Room for Velocity**: If you run a Velocity proxy network, players wait in a clean, built-in waiting room while logging in. You do not need to create an extra lobby server just for authentication.
*   **Bedrock Friendly**: Seamless support for Bedrock and mobile players connecting through Geyser or Floodgate.
*   **Smooth and Lag-Free**: Built to run quietly in the background without causing lag spikes or freezing your server.
*   **Two-Factor Authentication (2FA)**: Staff and players can link Google Authenticator to their account for extra security.
*   **Email Account Recovery**: Players who forget their passwords can easily reset them using their email address.
*   **Bot & Spammer Protection**: Comes with simple picture/chat captchas and limits how many accounts can join from the same internet connection.
*   **Real Skins for Everyone**: Restores official skins for players so nobody looks like a default Steve or Alex.
*   **Easy AuthMe Switch**: Upgrading from AuthMe? Move all your existing player accounts over with one simple command.

---

## Easy Setup Guide

### For a Single Server (Paper / Spigot)
1. Download `peyajAuth-Paper-1.6.9.jar`.
2. Place the file inside your server's `plugins/` folder.
3. Restart your server to generate the configuration files.
4. Open `plugins/peyajAuth/config.yml` to customize messages or settings if desired.

### For a Proxy Network (Velocity)
1. Place `peyajAuth-Velocity-1.6.9.jar` inside your Velocity proxy `plugins/` folder.
2. That's it! Velocity will handle logins and provide the built-in waiting room automatically.
3. If you want to use a shared database (like MySQL) to connect multiple servers, you can configure `database.yml`.
4. (Optional) You can customize the waiting room by dropping your own `spawn.schem` build file into the plugin folder.

---

## Commands & Permissions

### Player Commands

| Command | Shortcut | What it does | Who can use it |
| :--- | :--- | :--- | :--- |
| `/register <password> <confirm>` | `/reg` | Create a password for your account | Everyone |
| `/login <password>` | `/l` | Log into your account | Everyone |
| `/logout` | | Log out of your current session | Everyone |
| `/changepassword <old> <new>` | `/cp` | Change your password | Everyone |
| `/unregister <password>` | | Delete your account password | Everyone |
| `/disconnect` | | Leave the waiting room / server | Everyone |
| `/captcha <code>` | | Complete the anti-bot test | Everyone |
| `/email <add\|change\|remove\|confirm>` | | Set up a recovery email address | Everyone |
| `/2fa <setup\|confirm\|disable>` | | Turn on Google Authenticator | Everyone |

### Admin Commands

| Command | What it does | Permission |
| :--- | :--- | :--- |
| `/auth reload` | Reload all configuration files | OP |
| `/auth force <player>` | Manually log in or log out a player | OP |
| `/auth unregister <player>` | Remove a player's account password | OP |
| `/auth premium <player>` | Set a player to automatic paid login | OP |
| `/auth cracked <player>` | Set a player to password login | OP |
| `/auth info <player>` | View information about a registered account | OP |
| `/auth gui` | Open the in-game admin menu | OP |
| `/auth setspawn` | Set the login spawn point (Paper) | OP |
| `/auth spawn` | Teleport to the login spawn point (Paper) | OP |
| `/auth import <file.db>` | Import player accounts from an AuthMe database | OP |

---

## Planned Features (Roadmap)

*   **Discord Webhook Alerts**: Send alerts directly to your staff Discord channel when players register, fail logins, or when staff update accounts.
*   **In-Game Map QR Codes for 2FA**: Show a scannable QR code on a Minecraft map item for effortless Google Authenticator setup.

---

## Developer API

peyajAuth provides a dedicated, lightweight public API library (**`peyajAuth-API-1.6.9.jar`**, ~8 KB) containing all interfaces and event classes without any server logic. You can compile against it on Paper or Velocity:

### On Paper:
```java
import me.peyaj.peyajauth.api.PeyajAuthAPI;

PeyajAuthAPI api = PeyajAuthAPI.getInstance();

// Check if a player is logged in
boolean isLoggedIn = api.isAuthenticated(player);

// Check if a player joined with verified Java Premium
boolean isPremium = api.isPremium(player);
```

### On Velocity Proxy:
```java
import me.peyaj.peyajauth.api.PeyajAuthVelocityAPI;

PeyajAuthVelocityAPI api = server.getServicesManager()
    .query(PeyajAuthVelocityAPI.class)
    .get()
    .getProvider();

// Check if a player is logged in on the proxy
boolean isLoggedIn = api.isAuthenticated(player.getUniqueId());
```

For full setup guides, custom Bukkit events, and Velocity proxy events, visit the [Developer API Documentation](https://github.com/realpeyaj/peyajAuth/wiki/Developer-API).

---

## Server Statistics
[![bStats Paper](https://bstats.org/signatures/bukkit/peyajAuth.svg)](https://bstats.org/plugin/bukkit/peyajAuth/32544)
[![bStats Velocity](https://bstats.org/signatures/velocity/peyajAuth.svg)](https://bstats.org/plugin/velocity/peyajAuth/34033)

---

## License
Copyright © 2026. All rights reserved.
