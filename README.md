# peyajAuth

A high-performance, modular, and secure hybrid authentication solution for Spigot/Paper (1.21+ & 26.2+) and Velocity Proxy (3.0.0 - 4.x+).

![Java](https://img.shields.io/badge/Java-21-orange.svg)
![Platform](https://img.shields.io/badge/Platform-Paper%20%7C%20Velocity-blue.svg)
![Version](https://img.shields.io/badge/Version-1.6.1-green.svg)
![License](https://img.shields.io/badge/License-Proprietary-red.svg)
[![bStats](https://img.shields.io/bstats/servers/32544?color=blue)](https://bstats.org/plugin/bukkit/peyajAuth/32544)

> [!IMPORTANT]
> **Offline Mode Requirement**: Both the Velocity proxy (in `velocity.toml`) and your backend Spigot/Paper servers (in `server.properties`) must be configured in offline mode (`online-mode=false`). The plugin dynamically triggers online-mode authentication handshakes for verified premium players at the proxy gateway, while allowing cracked players to connect securely.

---

**peyajAuth** is a lightweight, robust, and secure hybrid authentication plugin built for modern Minecraft networks and standalone servers.

---

## Key Features

*   **Multi-Platform Integration**: Deploy as a standalone Spigot/Paper plugin or run as a unified Velocity proxy gateway. Both modules sync seamlessly using an SQLite, a shared MySQL, or MariaDB backend.
*   **Embedded Velocity Void Limbo**: Velocity installations bundle their own built-in, zero-dependency virtual void world limbo server. Unauthenticated players are trapped in a local loopback server (`127.0.0.1`) automatically without requiring the external plugin.
*   **True Hybrid Auto-Login**: Automatically distinguishes premium vs. cracked players. Instantly logs in premium players without passwords, while cracked players are prompted to register or login securely.
*   **Cryptography**: Supports industry-standard **Argon2id** and **BCrypt** hashing with customizable iteration, memory, and thread factors.
*   **Zero-Thread Lag**: Built entirely on asynchronous, non-blocking queries and fast **HikariCP** database connection pools to prevent main-thread TPS drops.
*   **Advanced Bot & Alt Protections**: Features GUI chest-click or chat-based Captcha gates, brute-force IP/account locks, and configurable registration limits per IP.
*   **Two-Factor Authentication (2FA)**: Restricts movement, commands, and chat for password-verified connections until they supply their Google Authenticator (TOTP) code.
*   **Offline Skin Retention**: Fetches and restores genuine Mojang skins for offline/cracked players using premium names.

---

## Installation & Setup

### For Standalone Paper Servers
1.  Download the latest compiled `peyajAuth-Paper-1.6.1.jar` from the release section.
2.  Drop the JAR into your server's `plugins/` directory.
3.  Restart to generate default configs inside `plugins/peyajAuth/` (`config.yml`, `messages.yml`, `database.yml`, `premium.yml`).

### For Velocity Proxy Networks
1.  Place `peyajAuth-Velocity-1.6.1.jar` in your Velocity `plugins/` folder.
2.  Drop `peyajAuth-Paper-1.6.1.jar` into the `plugins/` folder of all backend servers (Lobbies, Gamemodes).
3.  Configure all modules to point to the same MySQL or MariaDB database in `database.yml` to sync player sessions across the entire proxy network.
4.  On startup, the Velocity plugin will automatically extract and launch its embedded Limbo server inside `plugins/peyajauth/peyajlimboapi/` on a dynamic port for secure lobby redirection.
    *   **Custom Spawn Map**: The plugin extracts a default void platform. You can replace it with any custom map by dropping your own `.schem` file into `plugins/peyajauth/peyajlimboapi/` and naming it `spawn.schem`. The plugin automatically detects and normalizes WorldEdit nested structures on startup to prevent load crashes.

---

## Commands & Permissions

| Command | Aliases | Description | Permission | Default |
| :--- | :--- | :--- | :--- | :--- |
| `/register <password> <confirm>` | `/reg` | Register a new account password | `peyajauth.register` | Everyone |
| `/login <password>` | `/l` | Authenticate your active session | `peyajauth.login` | Everyone |
| `/logout` | | Log out of your account | `peyajauth.logout` | Everyone |
| `/changepassword <old> <new>` | | Change your current account password | `peyajauth.changepassword` | Everyone |
| `/captcha <code>` | | Solve chat captcha verification | *none* | Everyone |
| `/email <add\|change\|remove\|confirm\|show>` | | Manage recovery email links | `peyajauth.login` | Everyone |
| `/2fa <setup\|confirm\|disable\|verify>` | | Manage Google Authenticator 2FA settings | `peyajauth.login` | Everyone |
| `/auth reload` | | Reload all configuration files | `peyajauth.reload` | OP |
| `/auth force <player>` | | Force log a player in/out | `peyajauth.force` | OP |
| `/auth unregister <player>` | | Unregister a player's account | `peyajauth.unregister` | OP |
| `/auth premium <player>` | | Set player auth mode to premium | `peyajauth.force` | OP |
| `/auth cracked <player>` | | Set player auth mode to cracked | `peyajauth.force` | OP |
| `/auth info <player>` | | View registered player details | `peyajauth.info` | OP |
| `/auth gui` | | Open the interactive Admin chest GUI | `peyajauth.admin` | OP |
| `/auth setspawn` | | Set the lobby spawn location (Paper) | `peyajauth.admin` | OP |
| `/auth spawn` | | Teleport to the lobby spawn (Paper) | `peyajauth.admin` | OP |
| `/auth help` | | Display the administrative commands help menu | `peyajauth.admin` | OP |

---

## Developer API

You can programmatically query authentication states across both Spigot/Paper and Velocity modules.

### Querying on Velocity Proxy:
```java
import me.peyaj.peyajauth.api.PeyajAuthVelocityAPI;

// Access registration service
PeyajAuthVelocityAPI api = server.getServicesManager().query(PeyajAuthVelocityAPI.class).get().getProvider();

// Check if player has authenticated
boolean isLoggedIn = api.isAuthenticated(player.getUniqueId());

// Verify if username is already registered in database
api.isRegistered(player.getUsername()).thenAccept(registered -> {
    if (registered) {
        // ...
    }
});
```

### Querying on Paper Backend:
```java
import me.peyaj.peyajauth.api.PeyajAuthAPI;

// Check if player is logged in
boolean loggedIn = PeyajAuthAPI.getInstance().isAuthenticated(player);

// Check if player owns a premium account
boolean isPremium = PeyajAuthAPI.getInstance().isPremium(player);
```

---

## bStats Server Metrics
[![bStats Metrics](https://bstats.org/signatures/bukkit/peyajAuth.svg)](https://bstats.org/plugin/bukkit/peyajAuth/32544)

---

## License
Copyright © 2026. All rights reserved. 
Decompilation, reverse engineering, unauthorized redistribution, and editing of this compiled software are strictly prohibited.
