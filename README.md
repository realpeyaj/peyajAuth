# peyajAuth

A high-performance, secure, and modern authentication solution for Spigot & Paper (1.21+).

![Java](https://img.shields.io/badge/Java-21-orange.svg)
![Platform](https://img.shields.io/badge/Platform-Spigot%20%7C%20Paper-blue.svg)
![Version](https://img.shields.io/badge/Version-1.0-green.svg)
![License](https://img.shields.io/badge/License-Proprietary-red.svg)

---

**peyajAuth** is a lightweight, robust, and secure hybrid authentication plugin built for modern Minecraft servers. It provides automatic premium login validation, interactive GUI PIN pads, brute-force protections, and native Geyser/Floodgate Bedrock support.

---

## Features

*   **Premium Auto-Login**: Automatically checks if a player owns a genuine Mojang account and logs them in instantly—no password required.
*   **Bedrock/Floodgate Bypass**: Auto-login support for Bedrock players connecting through Geyser & Floodgate (verified via Xbox Live).
*   **GUI PIN Pad**: Optional chest-inventory virtual PIN pad. Secure registration and login without typing passwords in public or private chat.
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
    *   `config.yml` - Configure settings, PIN lengths, and sound toggles.
    *   `messages.yml` - Translate messages and customize prefix gradients.
    *   `database.yml` - Connect to MySQL or MariaDB database pools.

---

## Commands & Permissions

| Command | Aliases | Description | Permission | Default |
| :--- | :--- | :--- | :--- | :--- |
| `/register <password> <confirm>` | `/reg` | Register a new account PIN | `peyajauth.register` | Everyone |
| `/login <password>` | `/l` | Authenticate your active session | `peyajauth.login` | Everyone |
| `/logout` | | Log out of your account | `peyajauth.logout` | Everyone |
| `/changepassword <old> <new>` | | Change your current account PIN | `peyajauth.changepassword` | Everyone |
| `/captcha <code>` | | Solve chat captcha verification | *none* | Everyone |
| `/auth reload` | | Reload all configuration files | `peyajauth.reload` | OP |
| `/auth force <player>` | | Force log a player in/out | `peyajauth.force` | OP |
| `/auth unregister <player>` | | Unregister a player's account | `peyajauth.unregister` | OP |
| `/auth info <player>` | | View registered player details | `peyajauth.info` | OP |

---

## Developer API

Integrate `peyajAuth` into your own plugins easily:

```java
import me.peyaj.peyajauth.api.PeyajAuthAPI;

// Check if a player is authenticated
boolean loggedIn = PeyajAuthAPI.getInstance().isAuthenticated(player);

// Check if a player is premium
boolean isPremium = PeyajAuthAPI.getInstance().isPremium(player.getUniqueId());
```

---

## License & Terms

Copyright © 2026. All rights reserved. 
Decompilation, reverse engineering, unauthorized redistribution, and editing of this compiled software are strictly prohibited.
