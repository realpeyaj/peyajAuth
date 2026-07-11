# peyajAuth

A high-performance, secure, and modern authentication solution for Spigot & Paper (1.21+).

![Java](https://img.shields.io/badge/Java-21-orange.svg)
![Platform](https://img.shields.io/badge/Platform-Spigot%20%7C%20Paper-blue.svg)
![Version](https://img.shields.io/badge/Version-1.5.2-green.svg)
![License](https://img.shields.io/badge/License-Proprietary-red.svg)
[![bStats](https://img.shields.io/bstats/servers/32544?color=blue)](https://bstats.org/plugin/bukkit/peyajAuth/32544)

> **Important Requirement**: Your server must be running in offline mode (`online-mode=false` in your `server.properties` file) for the authentication system and premium auto-login handler to function correctly.

---

**peyajAuth** is a lightweight, robust, and secure hybrid authentication plugin built for modern Minecraft servers. It provides automatic premium login validation, secure password authentication, brute-force protections, and native Geyser/Floodgate Bedrock support.

---

## Why Choose peyajAuth?

*   **State-of-the-Art Security**: Features industry-standard **Argon2id** (with customizable memory, iteration, and thread factors) and **BCrypt** password hashing, protecting player credentials from advanced brute-force attacks.
*   **True Hybrid Auto-Login**: Automatically detects premium vs. cracked players using modern client-side UUID checks. Auto-logs in premium players while safely allowing cracked players using premium usernames to join and register/login with a password (completely avoiding the dreaded "Invalid Session" kicks).
*   **Offline Skin Retention**: Automatically fetches and applies genuine Mojang skins for offline/cracked players connecting with premium names, keeping your server looking authentic.
*   **Zero Main-Thread Lag**: Built completely with asynchronous non-blocking queries and fast **HikariCP** database connection pools to ensure bulk concurrent connections do not drop server TPS.
*   **Folia & Proxy Ready**: Features fully abstracted scheduling for native compatibility with multi-threaded server software (like **Folia**) and auto-detects BungeeCord/Velocity forwarding.
*   **Advanced Bot Protection**: Keeps bot networks out using custom interactive chest-click GUI and chat-based Captcha challenges.

---

## Dependencies & Requirements

*   **Java Version**: **Java 21** or higher.
*   **Server Platform**: Spigot, Paper, Purpur, or Folia (Minecraft 1.16 - 1.21.x supported).
*   **Soft Dependencies**:
    *   **Floodgate**: Required only if you want automatic login bypasses for Bedrock Edition players.
    *   **PlaceholderAPI**: Optional, for exposing player auth placeholders to other plugins.

---

## Features

*   **Premium Auto-Login**: Automatically checks if a player owns a genuine Mojang account and logs them in instantly—no password required.
*   **Bedrock/Floodgate Bypass**: Auto-login support for Bedrock players connecting through Geyser & Floodgate (verified via Xbox Live).
*   **Captcha Gateway**: Stop bot joins on your server with customizable Chat or GUI chest-click captchas.
*   **Brute-Force Protection**: Temporarily lock accounts or ban IPs automatically after repeated failed login attempts.
*   **IP Registration Limits**: Restrict the number of accounts that can be registered under a single IP to prevent alt-spam.
*   **Custom Sounds**: Queue distinct sound chimes on join reminders, captcha checks, correct entry, and lockouts.
*   **SQL Database Support**: SQLite enabled out of the box, with high-performance MySQL and MariaDB connection pools using HikariCP.

---

## Installation & Setup

1.  Download the latest compiled release from the official page.
2.  Drop the jar file into your server's `plugins/` directory.
3.  Restart your server to generate the default configuration files.
4.  Tune settings and messages inside `/plugins/peyajAuth/` files:
    *   `config.yml` - Configure settings, password rules, and sound toggles.
    *   `messages.yml` - Translate messages and customize prefix gradients.
    *   `database.yml` - Connect to MySQL or MariaDB database pools.

---

## Commands & Permissions

| Command | Aliases | Description | Permission | Default |
| :--- | :--- | :--- | :--- | :--- |
| `/register <password> <confirm>` | `/reg` | Register a new account password | `peyajauth.register` | Everyone |
| `/login <password>` | `/l` | Authenticate your active session | `peyajauth.login` | Everyone |
| `/logout` | | Log out of your account | `peyajauth.logout` | Everyone |
| `/changepassword <old> <new>` | | Change your current account password | `peyajauth.changepassword` | Everyone |
| `/captcha <code>` | | Solve chat captcha verification | *none* | Everyone |
| `/auth reload` | | Reload all configuration files | `peyajauth.reload` | OP |
| `/auth force <player>` | | Force log a player in/out | `peyajauth.force` | OP |
| `/auth unregister <player>` | | Unregister a player's account | `peyajauth.unregister` | OP |
| `/auth premium <player>` | | Set player auth mode to premium | `peyajauth.force` | OP |
| `/auth cracked <player>` | | Set player auth mode to cracked | `peyajauth.force` | OP |
| `/auth info <player>` | | View registered player details | `peyajauth.info` | OP |
| `/auth gui` | | Open the interactive Admin chest GUI | `peyajauth.admin` | OP |

---

## Developer API

Integrate `peyajAuth` into your own plugins easily:

```java
import me.peyaj.peyajauth.api.PeyajAuthAPI;

// Check if a player is authenticated
boolean loggedIn = PeyajAuthAPI.getInstance().isAuthenticated(player);

// Check if a player is premium
boolean isPremium = PeyajAuthAPI.getInstance().isPremium(player);

// Check if a player is connecting from Bedrock Edition (via Floodgate/Geyser)
boolean isBedrock = PeyajAuthAPI.getInstance().isBedrockPlayer(player);
```

---

## Server Metrics

[![bStats Metrics](https://bstats.org/signatures/bukkit/peyajAuth.svg)](https://bstats.org/plugin/bukkit/peyajAuth/32544)

---

## License & Terms

Copyright © 2026. All rights reserved. 
Decompilation, reverse engineering, unauthorized redistribution, and editing of this compiled software are strictly prohibited.
